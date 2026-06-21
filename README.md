# Roger's Design Systems

An anthology of **six design languages**, each a faithful, modern homage to a moment when software — or print — had an unmistakable point of view. Not screenshots: real **tokens, components, and live documentation** you can read, copy, and build with.

**Live → https://amosroger91.github.io/Roger-s-Design-Systems/**

| System | Era | Homage to | Live |
|---|---|---|---|
| **[Gilt](gilt/)** | 1925 | Art Deco / the machine age (Paris Exposition, Chrysler Building) | [↗](https://amosroger91.github.io/Roger-s-Design-Systems/gilt/) |
| **[Cairn](cairn/)** | 1930s–77 | WPA park posters, USGS topo maps, the NPS Unigrid | [↗](https://amosroger91.github.io/Roger-s-Design-Systems/cairn/) |
| **[Sonora](sonora/)** | 1995 | The '90s Taco Bell rebrand — neon dusk + Memphis confetti | [↗](https://amosroger91.github.io/Roger-s-Design-Systems/sonora/) |
| **[Nebula](nebula/)** | 2001 | The original Xbox dashboard (ships CSS + tokens) | [↗](https://amosroger91.github.io/Roger-s-Design-Systems/nebula/) |
| **[Bliss](bliss/)** | 2001 | Windows XP "Luna" (full component kit + live desktop) | [↗](https://amosroger91.github.io/Roger-s-Design-Systems/bliss/) |
| **[Aurora](aurora/)** | 2006 | Windows Vista / Aero glass, Frutiger optimism | [↗](https://amosroger91.github.io/Roger-s-Design-Systems/aurora/) |

Each system's docs page follows the same presentation: a sticky top bar, a scrollspy sidebar, and long-scroll sections (color, type, spacing, elevation, components with live + copyable code, accessibility, and a heritage timeline) — skinned entirely in that language's own palette and type.

## Structure

```
index.html          ← this landing page
<system>/index.html ← the documentation site for each language
<system>/README.md   ← per-system notes
nebula/ , bliss/     ← also ship .css / .tokens.json / .js companion files
```

Open any `index.html` in a browser — everything is self-contained (only Google Fonts load externally).

## License

Each system is a design study and homage — original evocations, **not affiliated** with any named brand. MIT licensed.

Built by Roger Hernandez.
