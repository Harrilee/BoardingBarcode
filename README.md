# Boarding Pass Barcode Generator

A free, fully client-side web tool that generates **IATA BCBP boarding pass barcodes** (PDF417 · Aztec · QR) and renders realistic boarding pass mockups. Works entirely in the browser — no server, no tracking, no data leaves your device.

🔗 **Live demo: <https://harrilee.github.io/BoardingBarcode/>**
🌏 [中文 README →](./README_cn.md)

![Screenshot](./screenshot.jpg)

---

## Use cases

- **Reconstruct a lost / unavailable boarding pass** — generate one yourself when the original is missing or never arrived
- **Add a flight to Apple Wallet / Google Wallet** — both apps accept BCBP-compliant PDF417 barcodes
- **Test barcode scanners and airline self-service apps** that consume IATA BCBP
- **Education** — inspect the BCBP M-format string side-by-side with the rendered barcode
- **Development** — try different ECC levels, symbol sizes, and barcode formats against your own decoder

### Quick start

1. Open the [live demo](https://harrilee.github.io/BoardingBarcode/)
2. Fill in the row: passenger name, PNR, departure / arrival airports (IATA codes), flight #, date, seat, sequence number
3. The boarding pass mockup updates instantly with a PDF417 barcode at the bottom
4. Scan it with the target app, or click **Print All** to print on paper

---

## Features

- **PDF417 · Aztec · QR** — three barcode formats covering all major airline systems
- **Multi-row table editor** — edit several boarding passes side-by-side, with one-click *Copy* or *New Blank* row
- **Realistic mockups** — every row renders as a paper-style boarding pass with the correct ATB2 aspect ratio (~2.4:1)
- **Bilingual UI** — English / 中文 toggle, auto-detected from browser language, persists in URL (`?lang=`)
- **Auto-save** — passenger data persists in `localStorage`; never transmitted
- **Print-ready** — print all generated passes with one click; CSS print rules force scannable black-on-white output
- **SEO-friendly** — proper hreflang, JSON-LD structured data, Open Graph cards for sharing
- **100% client-side** — no backend, no analytics that touch your data, no requests with passenger info

---

## How it works

The barcode rendering is powered by the [Zint](https://www.zint.org.uk/) open-source barcode library, compiled to **WebAssembly** via Emscripten. The UI layer is plain HTML + CSS + vanilla JavaScript — no build step, no framework, no npm.

When you edit a row, the JS assembles an IATA Bar Coded Boarding Pass (BCBP) string in the standard M-format:

```
M1DOE/JOHN           EXYZ123 ZRHSFOBA 1234 147F035A0001 100
```

…then hands it to the Wasm module which returns an SVG barcode that's blitted onto the boarding pass mockup.

---

## Run locally

No build step — just open the file:

```bash
git clone https://github.com/Harrilee/BoardingBarcode.git
cd BoardingBarcode
open index.html          # macOS
# xdg-open index.html    # Linux
# start index.html       # Windows
```

For development on the C / Wasm side, see `em_debug_build.bat` / `em_rel_build.bat` — those compile the Zint sources with Emscripten.

---

## Disclaimer

This tool generates barcodes using a **public IATA standard (BCBP / Resolution 792)**. It is intended for:

- Adding **your own** flights to your **own** airline accounts when an official pass isn't handy
- Testing barcode scanners and BCBP-compliant systems
- Education and development

Do not use it to misrepresent travel you didn't take, defraud loyalty programs, or impersonate other passengers. Use at your own risk.

---

## References

- [IATA BCBP Implementation Guide v4 (PDF)](http://www.iata.org/whatwedo/stb/documents/bcbp_implementation_guidev4_jun2009.pdf)
- [What's contained in a boarding pass barcode — Shaun Donnelly](https://shaun.net/whats-contained-in-a-boarding-pass-barcode/)
- [Aztec Code (Wikipedia)](https://en.wikipedia.org/wiki/Aztec_Code)
- [Zint barcode library](https://github.com/zint/zint)

## Credits

- Original project: [shooshx/BoardingBarcode](https://github.com/shooshx/BoardingBarcode)
- Barcode engine: [Zint](https://www.zint.org.uk/) (BSD)
- This fork (UI redesign, multi-pass editor, i18n, mockups): [Harrilee](https://github.com/Harrilee/BoardingBarcode)

## License

[MIT](./LICENSE)
