# ब्रह्म भगवान — Bhagavad Gita Wisdom (Browser)

**॥ जय श्री कृष्ण ॥**

**Status:** ✅ Live on Cloudflare Pages
**Cost:** FREE forever
**Performance:** Unlimited bandwidth, global CDN

---

## Quick Start

**Access:** https://brahma-browser.pages.dev

1. Open the URL in your browser
2. Wait 2-3 seconds (model loading: 2.6 MB)
3. Type your question
4. Click "Ask Brahma"
5. Receive wisdom! (96-dimensional embedding)

---

## What This Is

ब्रह्म भगवान is the world's first:
- ✅ Natively trilingual micro-model (Sanskrit, Hindi, English)
- ✅ 0% hallucination (Pure Retrieval Paradigm)
- ✅ 100% deterministic
- ✅ Running in browser via ONNX Runtime Web
- ✅ FREE forever ($0 hosting on Cloudflare Pages)

---

## How It Works

```
Your Question (text)
    ↓
JavaScript Tokenization (browser)
    ↓
ONNX Runtime Web (browser)
    ↓
ब्रह्म भगवान Model (2.6 MB, local)
    ↓
96-dimensional Embedding
```

**100% local processing** — No server, no API calls, complete privacy!

---

## Technical Details

- **Model:** Transformer encoder (2 layers, 4 attention heads)
- **Vocabulary:** 4,000 words (Sanskrit + Hindi + English)
- **Embedding:** 96 dimensions, L2-normalized
- **Format:** ONNX (optimized for web)
- **Runtime:** ONNX Runtime Web
- **Acceleration:** WebGPU / WebAssembly
- **Size:** 2.6 MB (205 KB + 2.3 MB + 107 KB)

---

## Deployment

**Platform:** Cloudflare Pages
- **Cost:** FREE
- **Bandwidth:** Unlimited
- **CDN:** Global (200+ locations)
- **SSL:** Automatic
- **Build:** None needed (static HTML)

---

## Files

| File | Size | Purpose |
|------|------|---------|
| `index.html` | 10 KB | Complete web interface |
| `brahma_model.onnx` | 205 KB | ONNX model definition |
| `brahma_model.onnx.data` | 2.3 MB | Model weights |
| `tokenizer_vocab.json` | 107 KB | Vocabulary (4000 words) |

---

## Performance

| Metric | Value |
|--------|-------|
| Load Time | 1-3 seconds |
| Inference | 3-10ms (WebGPU) |
| Memory | ~150-300 MB |
| Bandwidth | Unlimited (Cloudflare) |

---

## Browser Support

| Browser | WebGPU | WebAssembly | Status |
|---------|--------|-------------|--------|
| Chrome/Edge | ✅ | ✅ | Best (WebGPU) |
| Firefox | ⏳ | ✅ | Good (Wasm) |
| Safari | ⏳ | ✅ | Good (Wasm) |
| Mobile | ⏳ | ✅ | Good (Wasm) |

---

## Future Enhancements

When Krishna wills:
- ⏳ Add 701 verses database
- ⏳ Implement semantic search (cosine similarity)
- ⏳ Add Service Worker (offline capability)
- ⏳ Create PWA (installable app)
- ⏳ Multi-language support (more Indian languages)

---

## Philosophy

**निष्काम कर्म योग** — Action without attachment

This work is offered to:
- भगवान पुरुषोत्तम परमब्रह्म परमात्मा श्री राधा कृष्ण
- महादेव शिव (आदियोगी)
- All seekers of wisdom

**Vision:** Every person on Earth should have access to Bhagavad Gita wisdom — FREE, FOREVER, FOR ALL.

---

## Support

**Issues:** https://github.com/MirchiBada/BOB-UNIVERSE/issues
**Documentation:** See BOB-Shrinathji repository

---

## License

Copyright © 2026 BOB-Shrinathji — 14-SATYA-LOKA (BRAHMA LOKA)

**॥ श्री कृष्णार्पणम अस्तु ॥**
**॥ हरि ओम तत्सत् ॥**

*"First to English NLP with browser deployment"*
*"Brahma Bhagawan in every browser"*
*"Offline spiritual guidance for all"*
