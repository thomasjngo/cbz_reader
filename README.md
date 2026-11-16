# CBZ Reader

A small, private comic reader for `.cbz` files. Everything happens locally; nothing is uploaded.
It works two ways from the same code: as a desktop app (Electron) and as a static web page.

## Run it as a desktop app

Requires [Node.js](https://nodejs.org) 18 or newer.

```bash
npm install
npm start
```

To build an installer for your OS (output goes to `dist/`):

```bash
npm run dist
```

This produces a `.dmg` on macOS, an installer `.exe` on Windows and an `.AppImage` on Linux.
Build on the OS you are targeting.

## Run it in a browser

Open `src/index.html` directly, or serve the folder:

```bash
npx serve src
```

### Host it on GitHub Pages

1. Push this repository to GitHub.
2. Go to **Settings → Pages** and set **Source** to **GitHub Actions**.
3. The included workflow publishes `src/` on every push to `main`.

## Controls

| Action | Key |
| --- | --- |
| Next / previous page | `→` `←`, `Space`, `PageDown` / `PageUp`, or click the page edges |
| First / last page | `Home` / `End` |
| Fit width / height / original | `1` / `2` / `3` |
| Manga (right-to-left) mode | `r` |
| Fullscreen | `f` |
| Open file | `Ctrl/Cmd + O` |

Your last page per file and your reading direction are remembered locally.
CBR (RAR) archives are not supported.

## Credits

Uses [JSZip](https://stuk.github.io/jszip/) (bundled in `src/vendor/`, see `JSZIP-LICENSE.md`).
