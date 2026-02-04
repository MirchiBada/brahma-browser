# CLAUDE.md - AI Assistant Guide for brahma-browser

## Project Overview

**brahma-browser** (ब्रह्म भगवान) is a browser-based Bhagavad Gita wisdom application that runs a transformer model entirely client-side using ONNX Runtime Web. The application generates 96-dimensional embeddings from user queries in Sanskrit, Hindi, and English.

**Live URL:** https://brahma-browser.pages.dev

**Philosophy:** निष्काम कर्म योग (Action without attachment) - Free spiritual guidance for all.

## Architecture

```
User Query (text)
    ↓
JavaScript Tokenization (browser)
    ↓
ONNX Runtime Web (browser)
    ↓
Brahma Model (2.6 MB single-file ONNX)
    ↓
96-dimensional L2-normalized Embedding
```

**Key Design Decisions:**
- 100% client-side processing (no backend/API calls)
- Single-file ONNX model (weights embedded, no external .data file)
- Static site deployment (Cloudflare Pages)
- Zero hallucination guarantee (Pure Retrieval Paradigm)

## File Structure

```
brahma-browser/
├── index.html              # Main application (HTML + CSS + JS in single file)
├── brahma_model.onnx       # ONNX model (~2.6 MB, single-file with embedded weights)
├── tokenizer_vocab.json    # Vocabulary mapping (4000 words, ~107 KB)
├── wrangler.toml           # Cloudflare Pages configuration
├── index-backup.html       # Backup version (older, uses external .data file)
├── index-fixed.html        # Debug version with enhanced error handling
└── README.md               # Project documentation
```

## Technology Stack

| Component | Technology | Version/Details |
|-----------|------------|-----------------|
| ML Runtime | ONNX Runtime Web | v1.20.0 (via CDN) |
| Model | Transformer Encoder | 2 layers, 4 attention heads |
| Embedding | 96-dimensional | L2-normalized |
| Vocabulary | Custom tokenizer | 4000 words (Sanskrit + Hindi + English) |
| Hosting | Cloudflare Pages | Free tier, global CDN |
| Acceleration | WebGPU / WebGL / WebAssembly | Automatic fallback |

## Key Code Sections

### Model Loading (index.html:281-351)
The `init()` function handles:
1. ONNX Runtime Web verification
2. WebGPU/WebAssembly capability detection
3. Tokenizer loading from JSON
4. Model session creation with execution providers

```javascript
const sessionOptions = {
    executionProviders: ['webgl', 'wasm'],
    enableProfiling: false,
    enableCaching: true
};
session = await ort.InferenceSession.create('brahma_model.onnx', sessionOptions);
```

### Tokenization (index.html:255-279)
The `tokenizeQuery()` function:
- Splits text on whitespace and punctuation
- Maps words to token IDs using vocabulary
- Falls back to character-based hashing for unknown words
- Pads/truncates to fixed length of 48 tokens
- Uses BigInt for int64 tensor compatibility

```javascript
// Token IDs use BigInt for ONNX int64 compatibility
tokens.push(BigInt(tokenId));
```

### Inference (index.html:353-419)
The `askBrahma()` function:
- Creates int64 tensor with shape [1, 48]
- Runs inference via `session.run({input_ids: input})`
- Extracts embedding from `outputs.embedding`
- Calculates L2 norm for verification

## Development Workflow

### Local Development
```bash
# Serve locally (any static file server works)
python -m http.server 8000
# or
npx serve .
```

Open `http://localhost:8000` in browser.

### Testing Changes
1. Modify `index.html`
2. Hard refresh browser (Ctrl+Shift+R / Cmd+Shift+R)
3. Check browser console (F12) for debug output
4. Verify model loads and inference works

### Deployment
- **Automatic:** Push to main branch triggers Cloudflare Pages deployment
- **Manual:** `wrangler pages deploy .`

No build step required - static files served directly.

## Code Conventions

### HTML/CSS/JS Structure
- Single-file architecture: All HTML, CSS, and JS in `index.html`
- Inline `<style>` block for CSS (lines 8-174)
- Inline `<script>` block for JS (lines 215-423)
- No external dependencies except ONNX Runtime Web CDN

### JavaScript Patterns
- Global variables for session state: `session`, `tokenizer`
- Async/await for all asynchronous operations
- Try/catch with user-friendly error messages
- Debug logging via `log()` function to both console and UI

### Error Handling
- Graceful fallback for missing tokenizer
- Detailed error messages with troubleshooting steps
- Debug panel that shows on error

### CSS Conventions
- CSS custom properties not used (inline values)
- Mobile-responsive via flexbox and max-width
- Status states via CSS classes: `.loading`, `.ready`, `.error`, `.info`
- Purple gradient theme: `#667eea` to `#764ba2`

## Model Details

| Property | Value |
|----------|-------|
| Input | `input_ids` - int64 tensor [1, 48] |
| Output | `embedding` - float32 tensor [1, 96] |
| Sequence Length | 48 tokens (fixed) |
| Special Tokens | `<PAD>=0`, `<UNK>=1` |
| Normalization | L2-normalized output (norm ≈ 1.0) |

## Browser Compatibility

| Browser | WebGPU | WebGL | WebAssembly | Status |
|---------|--------|-------|-------------|--------|
| Chrome/Edge | Yes | Yes | Yes | Best (WebGPU preferred) |
| Firefox | Partial | Yes | Yes | Good |
| Safari | Partial | Yes | Yes | Good (fixed in recent commits) |
| Mobile | Varies | Yes | Yes | Good |

**Safari Compatibility Note:** Recent commits (15d6ff6, c902b30) fixed array length mismatch issues for Safari.

## Common Tasks

### Adding New Vocabulary Words
1. Update `tokenizer_vocab.json`
2. Add word to `word_to_id` mapping
3. Increment `vocab_size` if needed
4. Test with queries containing new words

### Modifying UI
- All styles in `<style>` block (lines 8-174)
- Container max-width: 700px
- Rounded corners: 10-20px border-radius
- Responsive padding: 20-40px

### Debugging Model Issues
1. Open browser DevTools (F12)
2. Check Console for error messages
3. Look at Network tab for file loading
4. Debug panel shows initialization steps

### Updating ONNX Runtime Version
Change CDN URL in `index.html`:
```html
<script src="https://cdn.jsdelivr.net/npm/onnxruntime-web@1.20.0/dist/ort.min.js"></script>
```

## Important Constraints

1. **Model Size:** Keep under 5MB for fast loading
2. **No Server:** All processing must be client-side
3. **Privacy:** No user data leaves the browser
4. **Cost:** Must remain deployable on free tier
5. **Offline Potential:** Future PWA support planned

## Git Commit History Context

Recent fixes focused on:
- Single-file ONNX format (no external .data file)
- Safari browser compatibility
- Enhanced error handling and debugging

## Related Resources

- **Issues:** https://github.com/MirchiBada/BOB-UNIVERSE/issues
- **ONNX Runtime Web:** https://onnxruntime.ai/docs/get-started/with-javascript.html
- **Cloudflare Pages:** https://pages.cloudflare.com/
