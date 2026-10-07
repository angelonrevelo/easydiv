<p align="center">
  <img src="icons/icon128.png" alt="EasyDiv icon" width="96">
</p>

# EasyDiv

**A Chrome extension that copies any part of any website as clean Tailwind, plain HTML+CSS, or React/JSX.**

See a nice navbar, pricing card or footer and want it in your own project?
Point EasyDiv at it, click, and copy. It reads the styles the browser actually
applied and turns them into idiomatic Tailwind classes — named colours like
`red-500` instead of raw `rgb(...)`, plus `hover:`, `md:` and `dark:` variants
pulled from the page's own stylesheets.

- **Grab a whole page in one click.** "Scrape Page" finds every reusable piece
  — headers, navs, forms, cards, buttons, lists — and files them into a dock you
  can filter by type.
- **Edit before you copy.** Open any capture full-screen, trim the HTML, and
  save it back.
- **Four copy formats.** Original HTML, Tailwind, Universal (self-contained
  inline styles that render anywhere), or JSX.
- **Peek inside other extensions.** A built-in viewer downloads any Chrome
  extension by ID or Web Store URL and shows its files and permissions.

Everything runs in your browser: no server, no account, no API key, no AI,
no telemetry.

## Install

```bash
git clone https://github.com/angelonrevelo/easydiv.git
```

1. Open `chrome://extensions`
2. Turn on **Developer mode** (top right)
3. **Load unpacked** → pick the `easydiv/` folder
4. Pin **EasyDiv** to the toolbar, or use the **EasyDiv** tab in DevTools

No `npm install` is needed to use it — that is only for the tests.

## Use it

| To… | Do this |
|---|---|
| Copy one element | Popup → **Activate Inspector** → hover (green outline) → click → **Copy ▾** on the dock item |
| Copy a whole page | Popup → **Scrape Page** → filter with the category pills → copy what you want |
| Tweak before copying | **View** on a dock item → **Edit** → **Apply to preview** (⌘/Ctrl+Enter) → **Save to dock** |
| Inspect an extension | Wrench icon → paste an extension ID or Web Store URL |
| Use Tailwind v4 or your own colours | Gear icon → pick v3/v4, paste your `tailwind.config.js` colours |

## Configuration

No `.env`. Settings (Tailwind version, custom palette) and captured components
are stored in Chrome's extension storage on your machine.

## How it works

```
 page element ──► freeze: computed styles, pseudo-elements, shadow DOM,
                  same-origin iframes, @keyframes, @font-face
                      │
                      ▼
             Tailwind emitter (hand-written, ~60 KB, no compiler)
             snap to the Tailwind scale · match palette · add hover:/md:/dark:
                      │
                      ▼
             dock ──► copy as HTML · Tailwind · Universal · JSX
```

It snapshots what the page *looks like*, not what it *does*: JavaScript
behaviour, canvas/WebGL content, and styles from cross-origin stylesheets
without CORS are not captured.

## Tests

```bash
npm install
npm test               # unit + detector (fast)
npm run test:e2e       # engine on real sites (Playwright)
npm run test:ext       # full extension in Chromium
npm run test:fidelity  # pixel-diff: capture vs. original
npm run test:all       # everything
```

## More

- [docs/internals.md](docs/internals.md) — what the engine does property by property, file map, test tiers, fidelity results, competitor comparison, known limitations
- [CHANGELOG.md](CHANGELOG.md) — release history

## License

MIT, as declared in `package.json` (the repo has no LICENSE file yet).
