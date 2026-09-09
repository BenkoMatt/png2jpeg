# PNG → JPEG

A fast, private, batch PNG-to-JPEG converter that runs entirely in your browser.

**Live site: https://benkomatt.github.io/png2jpeg/**

## Why

JPEG doesn't support transparency, and many platforms (marketplaces, CMSs, email
systems) silently reject or mangle PNGs. This tool converts a whole batch of PNGs
to clean JPEGs in one pass, with a quality slider and control over what color
replaces transparent areas.

## Features

- **Batch conversion** — drop in as many PNGs as you like, convert them all at once
- **Quality slider** (1–100) — see the size savings per file and in total
- **Transparency handling** — transparent areas are filled with white, black, or a
  custom color you pick (JPEG has no alpha channel)
- **Per-file downloads** or one **.zip** with everything
- **100% private** — conversion uses the browser's Canvas API; images never leave
  your device. No uploads, no accounts, no watermarks, no limits.
- Works offline once loaded. Dark mode follows your system.

## How it works

Each PNG is decoded with `createImageBitmap`, drawn onto a canvas over the
matte color you chose, and re-encoded with `canvas.toBlob('image/jpeg', q)`.
The zip bundle is built with [JSZip](https://stuk.github.io/jszip/) (loaded from
a CDN, with a graceful per-file download fallback if it's unavailable).

## Run locally

No build step. Serve the folder over HTTP (the file picker works on `file://`,
but serving is more realistic):

```sh
python3 -m http.server 8080
# → http://localhost:8080
```

## Browser support

Any modern browser (Chrome, Edge, Firefox, Safari). Clipboard paste and drag-and-drop
included.

## License

MIT — see [LICENSE](LICENSE).