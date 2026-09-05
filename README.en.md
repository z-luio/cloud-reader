# Cloud Reader

[简体中文](README.md)

A browser-based EPUB / TXT reader that runs locally and supports offline use. Download or clone this project, then open `txt.html` directly in a browser.

Current version: **v1.1.0** · [pre-update v1.0.0](https://github.com/z-luio/cloud-reader/releases/tag/v1.0.0) · [post-update v1.1.0](https://github.com/z-luio/cloud-reader/releases/tag/v1.1.0)

![Upload screen](assets/screenshots/upload.png)

![Reading screen](assets/screenshots/reader.png)

## Features

- Import `.epub`, individual `.txt`, multiple `.txt` files, or a TXT folder.
- Sort multiple TXT files naturally, treating each file as one chapter with continuous reading and table-of-contents navigation.
- Detect UTF-8, UTF-16LE, UTF-16BE, and GB18030/GBK TXT encodings automatically.
- Recognize common Chinese chapter headings; split long TXT files without headings into readable sections.
- Read EPUB metadata, chapter order, body content, and images.
- Navigate with a table of contents, keyboard shortcuts, and swipe gestures on touch devices.
- Read in a seamless long-page view that loads the next chapter near the bottom and reclaims distant chapter DOM nodes.
- Load multi-TXT chapters on demand with at most two concurrent preloads and bounded chapter/DOM caches.
- Show batch-import progress, support cancellation, and clean up stale tasks when switching books.
- Choose five built-in themes or a custom background color; adjust font size, font family, and line height.
- Save reading settings and progress locally in the browser. Book contents are not uploaded.

## Usage

1. Download this project and open `txt.html` in a supported browser.
2. Click the upload area, or drag one EPUB or TXT file onto it. You can also select multiple TXT files or a TXT folder.
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

Book content is parsed and rendered in the browser and is never uploaded. Reading settings and progress are stored with browser `localStorage`; clearing site data removes those records. Multi-TXT mode stores only file metadata and reading positions, loads chapters on demand, and uses bounded caches. TXT imports are limited to 2,000 files, 50 MB per file, and 512 MB total; content is HTML-escaped before rendering.

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

- This release imports one EPUB or a group of TXT files. Multi-TXT mode treats each file as one chapter and does not rescan each file for additional chapters.
- Source files are held by the browser session. After reloading the page, select the book again to open it.
- Streaming chapter indexing for one extremely large TXT file and full-text search are not included.
- Use a current version of Chrome, Edge, Firefox, or Safari.

## Version history

### v1.1.0 · Multi-TXT reading update

- Added multi-TXT selection, TXT folder import, and natural filename ordering.
- Added on-demand chapter loading, Promise deduplication, two-concurrent preloading, and bounded caches.
- Added import progress, cancellation, and 2,000-file / 50 MB-per-file / 512 MB-total limits.
- Strengthened book-switch task isolation, path-aware fingerprints, duplicate handling, and safe TXT rendering.

### v1.0.0 · Pre-update version

- Supported local reading for one TXT file or one EPUB.
- Included TXT encoding detection, chapter recognition, table of contents, themes, and reading progress.

## License

This project is released under the [MIT License](LICENSE). The bundled JSZip 3.10.1 dependency is also used under its optional MIT terms; see the [third-party notices](THIRD_PARTY_NOTICES.md).
