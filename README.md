# ECHO TYPOGRAPHY

**Subtractive typography.** Keyboard-driven. Monochrome. One HTML file.

🇯🇵 [日本語版](./README.ja.md)

---

## Concept

The canvas is already full. You don't type — you **carve**.
Negative space is the medium. Every keystroke is an act of subtraction.

A single HTML file, keyboard-only, pure monochrome.
Influenced by Constraint Systems — UI stripped to its essence.

## Run

No build step. Open `index.html` directly:

```bash
open index.html                   # macOS
# or serve locally:
python3 -m http.server 8080
```

First load fetches React, Tailwind, and Space Mono from CDN — online once.

## Controls

| Key       | Action                                  |
| --------- | --------------------------------------- |
| `H J K L` | move the cursor (vim-style)             |
| `SPACE`   | subtract / restore the cell (toggle)    |
| `ENTER`   | fill · cycle source word                |
| `S` / `B` | font size − / +                         |
| `I`       | invert black / white                    |
| `P`       | export current state as SVG             |
| `?`       | toggle the help panel                   |
| `ESC`     | close help                              |

A help panel opens on launch; any handled key dismisses it, `?` re-opens it.

## Files

```
echo_typography/
├── index.html       — the app (self-contained, ~390 lines)
├── README.md        — this file
└── README.ja.md     — Japanese version
```

## Stack

- **React 18** — via import map + `esm.sh`
- **Babel Standalone** — `data-type="module"` transpiles JSX to ESM in-browser
- **Tailwind CSS** — Play CDN, JIT with arbitrary values
- **lucide-react** — a single accent icon
- **Space Mono 700** — via Google Fonts

Runtime-only. No bundler, no `npm install`.

## Hackable points

Surfaced at the top of `index.html`:

- `SOURCES` — words cycled by `ENTER`
- `SIZE_MIN` / `SIZE_MAX` / `SIZE_STEP` — font-size bounds
- grain `opacity` — the only non-essential visual; tuned low
- `exportSVG` — vector export; PNG is trivial to add via canvas

State is a 2D array of `{ ch, hid }`. Fork freely.

## Design notes

- **1 text run per row** — each grid row is a single pre-formatted `<div>`, so several thousand cells stay fluid
- **cursor via `mix-blend-mode: difference`** — always visible against black bg, white characters, and both themes
- **layout-preserving resize** — `S` / `B` keep the carving pattern at the same `(row, col)` coordinates
- **film grain** — static SVG `feTurbulence`, desaturated, 11% opacity, overlay blend

## Browser support

Requires native import maps: Chrome 89+, Safari 16.4+, Firefox 108+.

## Philosophy

> 余計な装飾を削ぎ落とし、機能そのものが美しさを定義する。
> Strip away ornament; let function define beauty.

—

© kinoshita studio
