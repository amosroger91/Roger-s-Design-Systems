# NEBULA

A living-machine design system — translucent glass, bioluminescent green, and one beating core in the dark. A respectful, modern homage to the original Xbox dashboard (2001).

- **`nebula.css`** — the system: design tokens + components. Drop into any project.
- **`nebula.tokens.json`** — the same tokens as data, for JS theming / Style Dictionary / Figma tooling.
- **`nebula-design-language.html`** — the documentation site (open it in a browser).

Everything is namespaced — tokens are `--nb-*`, classes are `.nb-*` — and the stylesheet applies **no global reset** and styles **no bare element selectors**, so it drops into an existing codebase without collisions.

---

## Install

1. Link the stylesheet:

   ```html
   <link rel="stylesheet" href="nebula.css">
   ```

2. (Recommended) Link the fonts. The system falls back to `system-ui` if you skip this.

   ```html
   <link rel="preconnect" href="https://fonts.googleapis.com">
   <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
   <link href="https://fonts.googleapis.com/css2?family=Exo+2:wght@200;300;400;600&family=Hanken+Grotesk:wght@300;400;500;700&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
   ```

3. Opt a page or region into the dark theme by adding `.nb-root`:

   ```html
   <body class="nb-root">
     <button class="nb-btn nb-btn--primary">Launch</button>
   </body>
   ```

   `.nb-root` only sets background, text color, and base font. If you just want the
   **tokens** (e.g. to theme your own components), you don't even need it — the
   `--nb-*` custom properties live on `:root` and are available everywhere.

---

## Theming

The default palette is the modern bioluminescent green (`--nb-accent: #3aee84`).
Switch to the **authentic 2001 radioactive "apple green"** (`#7EB900` lineage) with a single attribute:

```html
<html data-nb-theme="2001"> … </html>
```

Toggle it from JS:

```js
const root = document.documentElement;
root.dataset.nbTheme = root.dataset.nbTheme === '2001' ? '' : '2001';
```

Because every component reads from semantic tokens, the whole UI re-tints. To make
your own theme, override the semantic roles in a scope of your choosing:

```css
[data-nb-theme="cyan"] {
  --nb-accent: #38e8ff;
  --nb-accent-rgb: 56, 232, 255;     /* keep the -rgb pair in sync for glows */
  --nb-accent-strong: #9af3ff;
  --nb-core: #e8feff;
  --nb-deep: #0a4a5a;
}
```

---

## Tokens

| Group | Examples | Notes |
|---|---|---|
| **Color (primitive)** | `--nb-green-50…900`, `--nb-ink-0…4`, `--nb-teal-400`, `--nb-amber-400`, `--nb-red-400` | Raw ramps. Prefer the semantic roles below in product code. |
| **Color (semantic)** | `--nb-bg`, `--nb-surface`, `--nb-text`, `--nb-text-dim`, `--nb-border`, `--nb-accent`, `--nb-success`, `--nb-warning`, `--nb-danger`, `--nb-info`, `--nb-focus` | What you should actually reference. |
| **Accent RGB** | `--nb-accent-rgb` (also `--nb-success-rgb`, etc.) | Comma triplets for `rgba(var(--nb-accent-rgb), 0.4)` glows. |
| **Type** | `--nb-font-display/sans/mono`, `--nb-text-2xs…4xl`, `--nb-text-display`, `--nb-weight-*`, `--nb-leading-*`, `--nb-tracking-*` | Three faces: cold display, warm UI, mono data. |
| **Space** | `--nb-space-1…24` | 4px base scale. |
| **Radius** | `--nb-radius-xs…2xl`, `--nb-radius-pill` | |
| **Elevation** | `--nb-shadow-1/2/3`, `--nb-shadow-glass`, `--nb-glow-sm/md/lg` | |
| **Motion** | `--nb-ease-organic/glass/out`, `--nb-dur-fast/base/slow/pulse` | Things breathe and drift; they don't snap. |
| **Z-index** | `--nb-z-base/raised/sticky/overlay/toast` | |
| **Layout** | `--nb-container`, `--nb-container-narrow` | |

`nebula.tokens.json` carries the same values (with `{group.name}` aliases) for tooling.

---

## Components

All class-based, all reading from tokens. Selected examples — see the docs page for live demos and full source.

```html
<!-- Buttons -->
<button class="nb-btn nb-btn--primary">Primary</button>
<button class="nb-btn nb-btn--secondary">Secondary</button>
<button class="nb-btn nb-btn--ghost">Ghost</button>
<button class="nb-btn nb-btn--danger">Delete</button>
<button class="nb-btn nb-btn--primary nb-btn--sm">Small</button>

<!-- Surfaces -->
<div class="nb-glass nb-card">
  <h3 class="nb-card__title">Frosted pane</h3>
  <p class="nb-card__body">Beveled, lit from above, translucent.</p>
</div>

<!-- Form field -->
<label class="nb-field">
  <span class="nb-label">Soundtrack name</span>
  <input class="nb-input" type="text" placeholder="Untitled (1)">
  <span class="nb-help">Stored in memory, counted in blocks.</span>
</label>

<!-- Switch -->
<label class="nb-switch">
  <input class="nb-switch__control" type="checkbox" checked>
  <span class="nb-switch__track"></span>
  <span class="nb-switch__label">Ambient audio</span>
</label>

<!-- Badges -->
<span class="nb-badge">alive</span>
<span class="nb-badge nb-badge--warning">degraded</span>
<span class="nb-badge nb-badge--danger">offline</span>

<!-- Meter -->
<div class="nb-meter"><span class="nb-meter__value" style="width:62%"></span></div>

<!-- Controller hint -->
<span class="nb-pad"><span class="nb-pad__key">A</span> select</span>
<span class="nb-pad nb-pad--b"><span class="nb-pad__key">B</span> back</span>
```

Component classes: `nb-glass`, `nb-surface`, `nb-card`, `nb-btn` (`--primary/secondary/ghost/danger`, `--sm/lg/icon/block`), `nb-field` / `nb-label` / `nb-input` / `nb-textarea` / `nb-help`, `nb-badge` (tones), `nb-tag`, `nb-switch`, `nb-meter` / `nb-blocks`, `nb-list`, `nb-tabs` / `nb-tab`, `nb-kbd`, `nb-pad`, `[data-nb-tip]` tooltip, `nb-divider`, `nb-orb` (identity).

---

## Accessibility

- Consistent `:focus-visible` ring on all interactive components (`--nb-focus`).
- `prefers-reduced-motion: reduce` disables the breathing/reveal/transition animations.
- The switch is a real `<input type="checkbox">`; tabs/lists are styled, not re-implemented — keep correct roles/`aria-*` in your markup.
- Accent-on-dark text passes WCAG AA at body sizes; use `--nb-text` / `--nb-text-dim` for prose, reserve the glow accent for emphasis and chrome.

---

## Credits & license

MIT licensed. A **design study, not affiliated with Microsoft or Xbox**; the typography, sound patterns, and the X-nexus mark are original evocations, not Microsoft assets.

With respect to the people behind the original screen: **Seton Kim** (dashboard / BIOS concept, produced at **REZN8**), **Brian Schmidt** (boot sound), and the original Xbox dashboard team — **Victor Blanco, Sakphong Chanbai, Bradford Christian, Jim Helm** — whose names hid in System Info for two decades.
