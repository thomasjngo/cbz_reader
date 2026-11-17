# Tenjin (CBZ Reader)

A fast, private comic and book reader that runs entirely in your browser. Nothing is ever uploaded: your files, covers and reading progress stay on your device.

**Live version:** https://thomasjngo.github.io/tenjin/

## Supported formats

| Format | Works out of the box? |
| --- | --- |
| **CBZ** (and ZIP archives of images) | Yes |
| **PDF** | Yes. The PDF engine (PDF.js) is downloaded from a CDN the first time you open a PDF, so that needs an internet connection. |
| **EPUB** (comic or manga EPUBs made of page images) | Yes. Pages follow the book's reading order. |
| **CBT** (tar archives of images) | Yes |
| **Loose images** (JPG, PNG, WebP, GIF, AVIF, BMP) | Yes. Select or drop several images and they open as one comic, sorted by name. |
| **CBR** (RAR) and **CB7** (7-Zip) | Optional. Add the three files in the `libarchive/` folder to your site (see below). |

Files are detected by their contents as well as their extension, so a mislabelled `.cbr` that is really a ZIP still opens.

## Features

### Reading
- **Page mode** shows one page at a time. **Scroll mode** is a continuous vertical scroll, which suits webtoons and long strips.
- **Two-page spreads** work in both modes. In Page mode, facing pages sit side by side. In Scroll mode, pages are laid out in rows of two, and wide spreads fill a full row. The first page can be shown alone like a cover (turn this off in Settings).
- **Seamless wide pages in Scroll mode.** If a mostly-portrait book has the occasional landscape double-page spread, then by default a spread is split into its two halves, stacked one after the other. Every page keeps the same text size and the same width, so the scroll never changes rhythm. Choose **Keep whole** in Settings to leave spreads intact. With 2 pages turned on, spreads simply take a full row instead.
- **Manga mode** reads right to left: arrow keys, click zones, the slider, spreads and split pages all flip.
- **Fit modes:** Width, Fit (the whole page), and Actual size.
- **Zoom** from 25% to 400%. Type a percentage in the toolbar field and press Enter, use the **+** and **−** buttons (10% steps), or use `Ctrl` + mouse wheel (zooms toward the cursor) or a trackpad pinch. Double-click the field to reset. Drag a zoomed page to move around it.
- **Smart scrolling:** `Space` scrolls down and turns the page when you reach the bottom. `Shift+Space` does the reverse.
- **Page previews:** a thumbnail strip along the bottom, or down the left side (your choice in Settings). Click a thumbnail to jump there. The current page, or both pages of a spread, is highlighted.
- **Page slider and jump box:** drag the slider, or type a page number (press `g`).
- **Page number indicator:** an optional "12 / 40" badge in the bottom-right corner.
- **Gentle transitions:** pages fade in as you turn them, and the library, dialogs and menus ease in. Transitions are switched off automatically if your system asks for reduced motion.
- **Themes:** automatic (follows your system), light or dark, with an Apple-inspired look: frosted toolbars, segmented controls, rounded cards and soft shadows.
- **Fullscreen** and a **hide toolbars** option (`h`, or click the middle of the page).
- Drag and drop a file anywhere on the page to open it.

### Library
- Click **Library** (or press `l`), then **Choose folder** to scan a folder and all its subfolders for CBZ, CBR, CB7, CBT, PDF and EPUB files.
- Each comic gets a **cover preview**, made from its first page. Covers are generated as you scroll and saved so they only need to be made once.
- **Reading progress** is tracked for every comic and shown as a progress bar with "Page 12 of 40", "Not started", or "Finished". Finished comics have a slightly greyed-out cover so unread ones stand out.
- **Resume where you left off:** opening a comic jumps back to the page you were on.
- **Continue reading** opens whatever you read most recently.
- **Search**, **filter** (All, Reading, Unread, Finished) and **sort** (Name, Recently read, Newest file).
- **Right-click a comic** (or long-press on a touch screen, or `Shift+F10` / the Menu key on a focused comic) for **Open**, **Mark as read**, **Mark as unread** and **Regenerate cover**.
- In Chrome and Edge, the folder is remembered. Next visit the app opens to your library, and you may be asked to click **Reconnect** once to re-grant access.

### Settings
Open **Settings** with the gear button or `s`:
- **Gap between pages in Scroll mode**, from 0 to 60 px (default 10).
- **Wide pages in Scroll mode:** split into two pages, or keep whole.
- **Page previews:** bottom or left side.
- **Page number** in the bottom-right corner, on or off.
- **First page alone** in two-page mode, on or off.
- **Reset all settings** to the defaults.

Your view choices are **remembered automatically** and applied every time you open a book: reading mode, fit mode, zoom level, two-page mode, Manga direction, theme, previews and everything in Settings.

## Controls

| Action | Key |
| --- | --- |
| Previous / next page | `←` `→` (flipped in Manga mode), or click the left / right edge of the page |
| Scroll down / up, turning the page at the edge | `Space` / `Shift+Space`, `PageDown` / `PageUp` |
| Scroll a little | `↑` `↓` |
| First / last page | `Home` / `End` |
| Zoom in / out / reset | `+` / `-` / `0` (10% steps) |
| Fit width / fit page / actual size | `1` / `2` / `3` |
| Two-page spreads | `d` |
| Page / Scroll mode | `v` |
| Page previews | `t` |
| Manga (right-to-left) mode | `r` |
| Hide or show toolbars | `h`, or click the middle of the page |
| Jump to a page number | `g` |
| Library | `l` (`Esc` returns to the book you were reading) |
| Settings | `s` |
| Fullscreen | `f` |
| Open a file | `Ctrl/Cmd + O` |
| Help | `?` |

## Where your data is stored

Everything is stored in your browser on your device, and nothing leaves it.

- **Settings and reading progress** are kept in the browser's local storage. Progress is matched by file name and size, so renaming or editing a file resets its progress.
- **Covers and the remembered folder** are kept in the browser's IndexedDB.
- Data is **per browser and per device** and does not sync. Clearing your browser's site data removes it.

## Browser support

- The reader works in current versions of Chrome, Edge, Firefox and Safari.
- Remembering your library folder uses the File System Access API, available in **Chrome and Edge**. In **Firefox and Safari** you pick the folder each visit; progress is still saved.

## Run it

Keep these files together in the same folder: `index.html` and `jszip.min.js`. To add CBR and CB7 support, also add the `libarchive/` folder (three files: `libarchive.js`, `worker-bundle.js` and `libarchive.wasm`).

**In a browser:** serve the folder (`npx serve .`) and open it. Opening `index.html` straight from disk works for CBZ, but CBR/CB7 support needs a web server.

**On GitHub Pages:**
1. Push the repository to GitHub and make it public.
2. Go to **Settings → Pages** and set **Source** to **GitHub Actions**.
3. The workflow in `.github/workflows/pages.yml` publishes the site on every push to `main`.

**As a desktop app (optional):** the repo can include a small Electron wrapper (`main.js` and `package.json`).

```bash
npm install
npm start
```

`main.js` must load `index.html` from the same place your copy of the file lives. Use `npm run dist` to build an installer for your operating system.

## Limits worth knowing

- Opening a file loads all of it into memory. Very large files (hundreds of MB) can be slow, and generating covers for a folder of them takes time. Covers are made one at a time to keep this manageable.
- PDFs are drawn page by page as images, so text is not selectable and very large PDFs are slower than CBZ.
- RAR and 7-Zip support is an optional add-on built on libarchive.js. Password-protected archives are not supported.
- In Scroll mode, pages load as you approach them and unload when far away. Spreads are detected as they load, so the scrollbar can shift slightly while page sizes are still being measured.
- The interface uses the system font on Apple devices (San Francisco) and Inter elsewhere. Inter is loaded from Google Fonts, so offline the app falls back to your system font.

## Credits and license

Uses [JSZip](https://stuk.github.io/jszip/) (MIT or GPLv3), [PDF.js](https://mozilla.github.io/pdf.js/) (Apache 2.0, loaded on demand) and, optionally, [libarchive.js](https://github.com/nika-begiashvili/libarchivejs) (MIT).

This project is released under the MIT License. See `LICENSE`.
