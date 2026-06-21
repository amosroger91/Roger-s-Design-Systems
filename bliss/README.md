# BLISS

A glossy, optimistic design system — friendly chrome you can see and want to press. A respectful, modern homage to the Windows XP **"Luna"** visual style (codename *Whistler*, 2001).

- **`bliss.css`** — the system: design tokens + components. Drop into any project.
- **`bliss.js`** — a zero-dependency behavior layer (tabs, menus, windows, the Start menu, dialogs, toasts) and a small `Bliss` API. Optional — components render without it.
- **`bliss.tokens.json`** — the same tokens as data, for JS theming / Style Dictionary / Figma tooling.
- **`bliss-design-language.html`** — the documentation site (open it in a browser).
- **`bliss-example-notepad.html`** — a standalone app (one window) built with the kit.
- **`bliss-example-desktop.html`** — a full desktop shell: window manager, taskbar, Start menu, live theming.

Everything is namespaced — tokens are `--bl-*`, classes are `.bl-*` — and the stylesheet applies **no global reset** and styles **no bare element selectors**, so it drops into an existing codebase without collisions. The three authentic Luna schemes — **blue** (default), **olive**, **silver** — are swapped by one attribute and reskin every component at once.

---

## Install

1. Link the stylesheet (and, optionally, the behavior layer):

   ```html
   <link rel="stylesheet" href="bliss.css">
   <script src="bliss.js" defer></script>
   ```

   Bliss uses the real XP faces — **Trebuchet MS** (titles) and **Tahoma** (UI) — which ship on Windows. On other platforms it falls back to `system-ui`, so nothing to load.

2. Opt a page or region into the Bliss surface by adding `.bl-root`:

   ```html
   <body class="bl-root">
     <button class="bl-btn bl-btn--default">OK</button>
   </body>
   ```

   `.bl-root` only sets the background, text color, base font, scrollbars, and focus rings. If you just want the **tokens** (to theme your own components), you don't even need it — the `--bl-*` custom properties live on `:root` and are available everywhere.

---

## Theming — the three Luna schemes

Set `data-bl-theme` on `.bl-root` (or any subtree) to recolor all the chrome at once:

```html
<body class="bl-root" data-bl-theme="olive"> … </body>
```

| scheme   | value      | accent     |
|----------|------------|------------|
| Blue     | `blue` *(default)* | `#1668e0` |
| Olive Green | `olive` | `#6f8a3e` |
| Silver   | `silver`   | `#6675a0` |

Or do it live in JS:

```js
Bliss.setTheme('silver');                 // themes the first .bl-root (or <body>)
Bliss.setTheme('blue', document.getElementById('panel'));  // theme a subtree
```

---

## The signature gloss

Luna's whole identity is one trick done consistently: a bright highlight up top, a quick step into a saturated body, a soft shadow at the base, and a thin lit lip at the very bottom. It's a reusable token:

```css
.my-bar {
  background: var(--bl-gloss-title),
              linear-gradient(180deg, var(--bl-title-hi), var(--bl-title-low));
  box-shadow: inset 0 1px 0 rgba(255,255,255,.55);
  border-radius: 7px 7px 0 0;
}
```

`--bl-gloss-sheen` (buttons), `--bl-gloss-title` (title bars/dialogs) and `--bl-gloss-bar` (taskbar) are the three prebuilt sheens.

---

## Components

All classes are prefixed `.bl-`. The ones marked **JS** become interactive when `bliss.js` is loaded.

| Area | Classes |
|------|---------|
| Layout / type | `.bl-container` `.bl-row` `.bl-col` `.bl-stack` `.bl-spread` `.bl-h1/2/3` `.bl-eyebrow` `.bl-mono` `.bl-kbd` `.bl-link` `.bl-divider` |
| Surfaces | `.bl-panel` `.bl-card` (`__head` `__body`) `.bl-bliss` (the wallpaper) |
| Buttons | `.bl-btn` + `--default` `--cta` `--ghost` `--link` `--icon` `--sm` `--lg` `--block` |
| Fields | `.bl-field` `.bl-label` `.bl-input` `.bl-textarea` `.bl-select` `.bl-search` `.bl-help` `.bl-spin` **JS** |
| Choices | `.bl-check` (checkbox/radio) **JS**, `.bl-switch` **JS**, `.bl-slider` **JS** |
| Containers | `.bl-tablist`/`.bl-tab`/`.bl-tabpanel` **JS**, `.bl-groupbox` |
| Data | `.bl-listview` **JS**, `.bl-tree` **JS**, `.bl-grid` **JS**, `.bl-tasks` **JS** |
| Status | `.bl-badge` (`--ok/info/warn/danger`) `.bl-tag` `.bl-progress` (`--marquee`) `.bl-tooltip` `.bl-balloon` **JS** `.bl-toast` **JS** |
| Chrome | `.bl-window` `.bl-titlebar` `.bl-winbtn` `.bl-menubar` **JS** `.bl-menu` **JS** `.bl-toolbar` `.bl-statusbar` `.bl-addressbar` |
| Overlays | `.bl-overlay`/`.bl-dialog` **JS** |
| Desktop | `.bl-desktop` `.bl-icon` `.bl-taskbar` `.bl-startbtn` `.bl-startmenu` `.bl-tray` **JS** |

### Example: a button + a checkbox

```html
<button class="bl-btn bl-btn--default">Save</button>

<div class="bl-check" role="checkbox" aria-checked="true" tabindex="0">
  <span class="bl-check__box">
    <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="3"><path d="M5 12l5 5L20 6"/></svg>
  </span>
  Remember me
</div>
```

### Example: a dialog

```html
<button class="bl-btn" data-bl-open="#hello">Open</button>

<div class="bl-overlay" id="hello">
  <div class="bl-dialog">
    <div class="bl-titlebar"><span class="bl-titlebar__title">Hello</span>
      <div class="bl-winbtns"><span class="bl-winbtn bl-winbtn--close" data-bl-close>×</span></div></div>
    <div class="bl-dialog__body">Built from tokens, themed by the active scheme.</div>
    <div class="bl-dialog__footer"><button class="bl-btn bl-btn--default" data-bl-close>OK</button></div>
  </div>
</div>
```

---

## `bliss.js` API

| call | does |
|------|------|
| `Bliss.init(root = document)` | (re)wire components inside `root` — call after injecting markup |
| `Bliss.setTheme(name[, el])` | apply a Luna scheme |
| `Bliss.toast(str \| {title, body, icon, timeout})` | show a notification toast |
| `Bliss.openDialog(elOrSel)` / `Bliss.closeDialog(...)` | overlay dialogs |
| `Bliss.openWindow(elOrSel)` / `Bliss.closeWindow(...)` | desktop windows |
| `Bliss.on(event, fn)` | listen for `theme`, `window:open`, `window:close` |

**Data hooks:** `data-bl-open="#dlg"`, `data-bl-close`, `data-bl-menu="#m"`, `data-bl-context="#m"`, `data-bl-open-window="#w"`, `data-bl-min/max/close` (window buttons), `data-bl-tasklist`, `data-bl-clock`.

A window manager activates automatically for any `.bl-desktop`: windows are draggable by their title bars, focus brings them forward (and dims the rest, as XP did), and the taskbar tracks what's open.

---

## Accessibility

- Color is never the only signal — status pairs a dot with a label; selections carry a visible focus rectangle (the authentic dotted XP rect, light on chrome and dark on the face).
- Checkboxes, radios, tabs, switches and windows respond to `Space`/`Enter`/arrows; `Esc` closes menus, dialogs and the Start menu.
- All motion (the Start-menu pop, marching progress, toasts) collapses under `prefers-reduced-motion`.
- A `@media print` block hides the taskbar, menus and toasts.

---

## License

MIT. A design study and homage; not affiliated with Microsoft or Windows. "Windows XP" and "Luna" are referenced descriptively.
