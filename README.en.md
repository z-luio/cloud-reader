# Cloud Reader

[简体中文](README.md)

A browser-based EPUB / TXT reader that runs locally and supports offline use. Download or clone this project, then open `txt.html` directly in a browser.

![Upload screen](assets/screenshots/upload.png)

![Reading screen](assets/screenshots/reader.png)

## Features

- Import `.epub` files and individual `.txt` files.
- Detect UTF-8, UTF-16LE, UTF-16BE, and GB18030/GBK TXT encodings automatically.
- Recognize common Chinese chapter headings; split long TXT files without headings into readable sections.
- Read EPUB metadata, chapter order, body content, and images.
- Navigate with a table of contents, keyboard shortcuts, and swipe gestures on touch devices.
- Read in a seamless long-page view that loads the next chapter near the bottom and reclaims distant chapter DOM nodes.
- Choose five built-in themes or a custom background color; adjust font size, font family, and line height.
- Save reading settings and progress locally in the browser. Book contents are not uploaded.

## Usage

1. Download this project and open `txt.html` in a supported browser.
2. Click the upload area, or drag one EPUB or TXT file onto it.
3. Open the table of contents to select a chapter, or scroll to read.
4. Use the floating toolbar on the right for the table of contents, night mode, reading settings, return to the upload screen, and jump-to-top.

### Keyboard and touch controls

| Control | Action |
| --- | --- |
| `←` / `→` | Previous / next chapter |
| `Space`, `PageDown` | Scroll down one page |
| `PageUp` | Scroll up one page |
| `T` | Open the table of contents |
| `N` | Toggle night mode |
| `B` | Return to the upload screen |
| `M` | Show or hide the right toolbar |
| `Tab` | Pin or unpin the right toolbar |
| Swipe left / right | Change chapter on touch devices |

## Privacy and dependencies

Book content is parsed and rendered in the browser. Reading settings and progress are stored with browser `localStorage`; clearing site data removes those records.

When an EPUB is imported, Cloud Reader tries the fixed JSZip CDN version with SHA-512 Subresource Integrity when the browser reports that it is online. If the browser is offline, the request times out, loading fails, or integrity verification fails, it automatically uses the identical bundled copy in `vendor/`. TXT reading does not load JSZip.

## Project layout

```text
cloud-reader/
├── txt.html                  # Standalone reader; open directly in a browser
├── assets/screenshots/       # Real UI screenshots used by the READMEs
├── LICENSE                   # MIT License for this project
├── THIRD_PARTY_NOTICES.md    # JSZip MIT license notice
├── vendor/
│   └── jszip-3.10.1.min.js   # Verified bundled EPUB dependency
├── README.md                 # Simplified Chinese documentation
└── README.en.md              # English documentation
```

## Scope and limitations

- This release imports one EPUB or one TXT file at a time. Multi-file chapter import, chapter manifests, and full-text indexing are not included.
- Source files are held by the browser session. After reloading the page, select the book again to open it.
- Use a current version of Chrome, Edge, Firefox, or Safari.

## License

This project is released under the [MIT License](LICENSE). The bundled JSZip 3.10.1 dependency is also used under its optional MIT terms; see the [third-party notices](THIRD_PARTY_NOTICES.md).
