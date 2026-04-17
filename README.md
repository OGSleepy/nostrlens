![nostrlens preview](og-preview.png)

# nostrlens

**Search text inside images on Nostr using OCR.**

🔍 **Live at [nostrlens.pages.dev](https://nostrlens.pages.dev)**

nostrlens connects to your Nostr relays, fetches image posts, and runs optical character recognition entirely in your browser. Search through the extracted text to find any image by what's written inside it. No server, no backend, no data ever leaves your device.

---

## Features

### Identity & Login
- **NIP-07 extension support** — one-click login with Alby, nos2x, or Amber. Your keys never touch the page.
- **npub login** — paste any `npub1…` to load a public identity
- **NIP-05 resolution** — enter `you@domain.com` and it resolves automatically to a pubkey
- Your NIP-65 relay list is fetched automatically on login

### Search
- **Full-text OCR search** across all indexed images
- **Phrase search** — wrap in quotes: `"exact phrase"`
- **AND search** — space-separated: `bitcoin price` matches images containing both words
- **OR search** — `lightning OR lnbc` matches either
- **Shareable URLs** — searches update the URL (`?q=your+query`) so you can copy and share results
- Filter by **All · Last 7 days · Last 30 days · My posts**

### Indexing
- Configurable **fetch limit** — 100 / 250 / 500 / 1000 events
- **Pause / Resume** OCR mid-batch without losing progress
- **Hide images with no text** toggle to keep results clean
- Index **persists across sessions** via localStorage — your OCR work is never wasted
- Live grid updates as images are processed

### Results
- npub displayed on every card instead of raw hex
- **View on Nostr ↗** button in the modal — jumps directly to the original post on njump.me
- **Open image ↗** button to view the full-resolution original
- **Export JSON** — download all indexed images (or just search results) with URL, OCR text, author npub, timestamp, and njump link

---

## How to use

1. **Login** — click "Connect with Extension" if you have Alby/nos2x/Amber, or paste your `npub1…` or `user@domain.com`
2. **Connect** — your NIP-65 relay list loads automatically; click **Connect all** to open WebSocket connections
3. **Fetch + OCR** — choose a fetch limit, hit the button, and watch the grid fill up as images are indexed
4. **Search** — type any word or phrase and press Enter or click Search
5. **Explore** — click any image card to see the full extracted text and jump to the original Nostr post

---

## Tech

| Piece | What it does |
|---|---|
| [nostr-tools v2.7](https://github.com/nbd-wtf/nostr-tools) | NIP-19 key encoding, event handling |
| [Tesseract.js v5.1](https://tesseract.projectnaptha.com/) | In-browser OCR via WebAssembly |
| NIP-07 (`window.nostr`) | Browser extension login (Alby, nos2x, Amber) |
| Native WebSocket | Relay connections — no extra library |
| `localStorage` | Index persists across sessions |

No build step, no framework, no dependencies to install. It is a single HTML file.

---

## Privacy

- No private keys are ever accepted or stored — login is via `npub` or NIP-07 extension only
- All OCR processing happens locally in your browser via WebAssembly
- The index lives in your browser's `localStorage` and never leaves your device
- No analytics, no tracking, no external requests beyond your chosen relays and CDN scripts loaded on page open

---

## Deployment

This project is a single `index.html` file plus `og-preview.png` for link previews. It runs on any static host with zero configuration.

**Cloudflare Pages**

1. Push `index.html` and `og-preview.png` to a GitHub repo
2. Go to Cloudflare Dashboard → Workers & Pages → Create → Pages
3. Connect your GitHub repo
4. Set framework preset to **None**, leave build command and output directory blank
5. Click **Save and Deploy**

Cloudflare redeploys automatically on every push.

---

## Files

```
index.html       — the full app (v1.0)
og-preview.png   — social preview image for link unfurling on Nostr, iMessage, etc.
README.md        — this file
```

---

## License

MIT
