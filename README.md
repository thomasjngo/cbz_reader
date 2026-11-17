# CBZ Reader

A fast, private comic reader for `.cbz` files that runs entirely in your browser. Nothing is ever uploaded: your comics, covers and reading progress stay on your device.

**Live version:** https://thomasjngo.github.io/cbz_reader/

## Features

### Reading
- **Page mode** shows one page at a time. **Scroll mode** is a continuous vertical scroll, which suits webtoons and long strips.
- **Two-page spreads** show facing pages side by side. The first page is shown alone like a cover (this can be turned off), and wide pages are always shown on their own.
- **Manga mode** reads right to left: arrow keys, click zones, the slider and spreads all flip.
- **Fit modes:** Width, Fit (the whole page), and Actual size.
- **Zoom** from 25% to 400% with the toolbar, keyboard, `Ctrl` + mouse wheel (zooms toward the cursor) or a trackpad pinch. Drag a zoomed page to move around it.
- **Smart scrolling:** `Space` scrolls down and turns the page when you reach the bottom. `Shift+Space` does the reverse.
- **Page previews:** a thumbnail strip along the bottom. Click one to jump there. The current page, or both pages of a spread, is highlighted.
- **Page slider and jump box:** drag the slider, or type a page number (press `g` to focus the box).
- **Page number indicator:** an optional "12 / 40" badge in the bottom-right corner (turn it on in Settings).
- **Themes:** automatic (follows your system), light or dark.
- **Fullscreen** and a **hide toolbars** option (`h`, or click the middle of the page) for distraction-free reading.
- Drag and drop a `.cbz` anywhere on the page to open it.

### Library
- Click **Library** (or press `l`), then **Choose folder** to scan a folder and all its subfolders for `.cbz` files.
- Each comic gets a **cover preview**, made from its first page. Covers are generated as you scroll and are saved so they only need to be made once.
- **Reading progress** is tracked for every comic and shown as a progress bar with "Page 12 of 40", "Not started", or "Finished".
- **Resume where you left off:** opening a comic jumps back to the page you were on.
- **Continue reading** button opens whatever you read most recently.
- **Search**, **filter** (All, Reading, Unread, Finished) and **sort** (Name, Recently read, Newest file).
- **Right-click a comic** (or long-press on a touch screen, or press `Shift+F10` / the Menu key on a focused comic) for:
  - **Open**
  - **Mark as read**
  - **Mark as unread**
  - **Regenerate cover**
- In Chrome and Edge, the folder is remembered. Next visit the app opens to your library, and you may be asked to click **Reconnect** once to re-grant access.

### Settings
Open **Settings** with the gear button or `s`:
- **Gap between pages in Scroll mode**, from 0 to 60 px.
- **Page number in the bottom-right corner**, on or off.
- **First page alone in two-page mode**, on or off.
- **Reset all settings** to the defaults.

Your view choices are **remembered automatically** and applied every time you open a book: reading mode (Page or Scroll), fit mode, zoom level, two-page mode, Manga direction, theme, page previews, and everything in Settings.

## Controls

| Action | Key |
| --- | --- |
| Previous / next page | `←` `→` (flipped in Manga mode), or click the left / right edge of the page |
| Scroll down / up, turning the page at the edge | `Space` / `Shift+Space`, `PageDown` / `PageUp` |
| Scroll a little | `↑` `↓` |
| First / last page | `Home` / `End` |
| Zoom in / out / reset | `+` / `-` / `0` |
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

- **Settings and reading progress** are kept in the browser's local storage. Progress is matched by file name and size, so renaming or editing a comic resets its progress.
- **Covers and the remembered folder** are kept in the browser's IndexedDB.
- Data is **per browser and per device** and does not sync. Clearing your browser's site data removes it.

## Browser support

- The reader works in current versions of Chrome, Edge, Firefox and Safari.
- Remembering your library folder uses the File System Access API, which is available in **Chrome and Edge**. In **Firefox and Safari** you pick the folder each visit; progress is still saved.
- Only `.cbz` files are supported. `.cbr` (RAR) archives are not.

## Run it

**In a browser:** open `index.html` directly, or serve the folder:

```bash
npx serve .
```

Keep `index.html` and `jszip.min.js` together in the same folder.

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

- Opening a comic loads the whole `.cbz` into memory. Very large files (hundreds of MB) can be slow, and generating covers for a folder of them takes time. Covers are made one at a time to keep this manageable.
- In Scroll mode, pages load as you approach them and unload when far away. The scrollbar can shift slightly while page heights are still being measured.
- The Figtree font is loaded from Google Fonts. Offline, the app falls back to your system font.

## Credits and license

Uses [JSZip](https://stuk.github.io/jszip/) to read `.cbz` archives, bundled as `jszip.min.js`. JSZip is dual-licensed under MIT or GPLv3.

This project is released under the MIT License. See `LICENSE`.
