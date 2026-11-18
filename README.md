# BigBar

**BigBar — Customizable large scroll bar for Windows**

A big, always-on-top scroll bar that sits on the edge of your screen and scrolls the window you last clicked — browsers, Word, Excel, PDF readers, Notepad, anything that exposes a scrollbar. Click it and it goes to the top or the bottom; drag the knob and the page scrolls proportionally. It never steals focus, and it stays above every other window.

Windows 7 SP1+ / 10 / 11 · single small exe · silent install · MIT licensed.

**Website: [www.bigbar.me](http://www.bigbar.me)** — browse and download skins, grab the installer, read the help pages.

**[Download »](https://github.com/YahooEatApple/BigBar/releases/latest)** · **[Skins »](http://www.bigbar.me/skins)** · **[Help »](http://www.bigbar.me/help)** · **[Docs site »](https://yahooeatapple.github.io/BigBar/)**

![BigBar with a dog skin](docs/screenshots/02-skin-puppy.png)

## Why

Thin, low-contrast scrollbars are hard to find and harder to grab — especially on high-DPI screens and when the window is not in the foreground. BigBar gives you one big, visible target on the screen edge that always controls the last-clicked window.

## What you get

- **A** — click to jump to the top of the document
- **K** — drag to scroll proportionally; hand cursor on hover, grabbing hand while dragging (even outside the bar)
- **B** — click to jump to the end
- **F** — the track, split into two segments at the knob's centre (A→K and K→B), each with its own skin block; the knob floats on top
- **Six anchor positions** — right-center / right-top / right-bottom / left-center / left-top / left-bottom, each with its own distance from the screen edge (px or %)
- **Always on top** — permanently, without stealing keyboard focus (no toggle in the menu)
- **Skins** — one JSON file per skin with CSS-like blocks for `pageup` / `pagedown` / `thumb` / `track` / `upper-track` / `lower-track` (old A / B / K / F / F1 / F2 still accepted), cursors, hover states, per-language names, and the `width` / `height` / `position` / `distance` / `limit` size objects in `tool.style`
- **Three languages** in the menu and tray: English / 中文 / Español
- **Menu** — Skin (first row) / Width / Height / Position / Distance / Opacity / Sound / Hide; the four size rows are sub-menus showing the current value plus an arrow, and adjusting position & height uses on-bar confirm / cancel buttons
- **Tray icon** with the same menu; the show / hide item has no hotkey (the old `Ctrl`+`Alt`+`S` shortcut was removed)
- **Add skin by code** — enter a skin code (≤ 16 chars), download `http://www.bigbar.me/skin/<code>` and unpack it into `%AppData%\BigBar\skins`, overwriting the local copy if it already exists

| Skin | North-land | Menu |
| --- | --- | --- |
| ![](docs/screenshots/04-skin-default.png) | ![](docs/screenshots/03-skin-northern-light.png) | ![](docs/screenshots/08-menu-en.png) |

## Install

1. Download `BigBar-Setup-1.1.6.exe` from Releases and run it.
2. It installs to `%LocalAppData%\Programs\BigBar`, creates desktop + Start-menu shortcuts and enables auto-start.
3. Silent install: `BigBar-Setup-1.1.6.exe /silent`
4. Uninstall: Settings → Apps → **BigBar**, or `Uninstall.exe /uninstall`

## Skins

Skins live in `%AppData%\BigBar\skins`. A default skin plus three samples are written there on first run.

```json
{
  "name": "MySkin",
  "language": { "en": "My Skin", "zh": "我的皮肤", "es": "Mi Piel" },
  "tool": [
    { "action": "default", "style": {
        "width":    { "default": "100px", "large": "100px", "medium": "70px", "small": "50px" },
        "height":   { "default": "600px", "large": "70%",   "medium": "50%", "small": "30%" },
        "position": { "default": "right-center" },
        "distance": { "default": "30px", "large": "50px", "medium": "30px", "small": "0px" },
        "limit":    { "max-height": "90%", "min-height": "400px" } } }
  ],
  "buttons": [
    { "name": "pageup", "action": "default",
      "style": {
        "cursor": "pointer",
        "height": "80px",
        "background-image": "url(MySkin/a.png)",
        "background-repeat": "no-repeat",
        "background-size": "cover",
        "background-position": "0px 0px"
      },
      "mouseover": { "style": { "background-image": "url(MySkin/a_hover.png)" } }
    },
    { "name": "thumb", "style": { "cursor": "pointer", "height": "120px" } },
    { "name": "upper-track", "style": { "background-image": "url(MySkin/track_top.png)", "background-repeat": "repeat-y" } },
    { "name": "lower-track", "style": { "background-image": "url(MySkin/track_bottom.png)", "background-repeat": "repeat-y" } }
  ]
}
```

`background-repeat` follows standard CSS (`repeat-x` / `repeat-y` / `no-repeat`), `background-position` accepts negative and split values, `background-size` accepts `auto` / `cover` / `100% auto`. `tool.style` holds `width` / `height` / `distance` as four-step objects (`default` / `large` / `medium` / `small`), `position` as one of the six anchors (`right-center` / `right-top` / `right-bottom` / `left-center` / `left-top` / `left-bottom`), and `limit` as `max-height` / `min-height`. Switching a skin reloads its files, images and size immediately.

Files you edit yourself are never overwritten by an update: built-in skins are only upgraded when they carry the program's own marker. If a skin ever gets replaced, a numbered `*.bakN` copy stays next to it.

## Files & settings

| Item | Path |
| --- | --- |
| Program | `%LocalAppData%\Programs\BigBar\BigBar.exe` |
| Settings | `HKCU\Software\BigBar` |
| Skins | `%AppData%\BigBar\skins` |
| Sounds | `%AppData%\BigBar\sounds` |
| Log | `%TEMP%\BigBar.log` |

Upgrading from the old name (`Gunbar`, earlier `BigScrollBar`)? Settings and skins are inherited and copied on first start — see [docs/使用说明.md](docs/使用说明.md) for the full Chinese manual, including the migration notes.

## Known limits

- Chromium-based and some UWP apps do not expose standard scroll info; exclusive full-screen Direct3D windows cannot be covered by a normal topmost window.
- Windows SmartScreen may warn because the build is not code-signed yet.

## License

MIT. See [LICENSE](LICENSE).
