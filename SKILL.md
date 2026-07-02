---
name: hacker-ui
description: >-
  Toms Haus-Designsystem für dunkle Hacker-/Ops-UIs (Web-Frontends, Dashboards,
  Feed-Seiten, Portale). Drei Themes: "cyberdeck" (Neon-HUD, Default),
  "midnight-ops" (professionell-ruhig), "phosphor" (Amber-CRT-Retro). Nutzen bei JEDEM Bau
  oder Redesign einer UI in diesem Homelab (Jarvis-Feed, Portal-Seiten,
  Status-/Admin-Seiten, neue Web-Apps), wenn keine andere Design-Vorgabe gilt.
---

# hacker-ui — dunkles Ops-Designsystem (3 Themes)

Einheitliche Design-Sprache für alle selbstgebauten Web-UIs: dunkel, technisch,
akzentfarben-getrieben. **Immer genau EIN Theme pro App** — nie mischen.

## Theme-Wahl (Entscheidungsregel)

| Theme | Wann | Referenz |
|---|---|---|
| **cyberdeck** (Default) | Toms Standard-Look. Wenn nichts anderes gesagt ist → das hier. Neon-HUD, Status-Walls, Dashboards, Feeds. | [themes/cyberdeck.md](themes/cyberdeck.md) |
| **midnight-ops** | Wenn es betont ruhig/seriös/kontrastsicher sein soll (dichte Admin-Tabellen, viel Fließtext, WCAG-AAA-Anspruch). | [themes/midnight-ops.md](themes/midnight-ops.md) |
| **phosphor** | Retro-/Terminal-Charme: CLI-artige Tools, Log-Viewer, Diagnose-Seiten, Einzweck-Utilities. | [themes/phosphor.md](themes/phosphor.md) |

**Vor dem Implementieren die Theme-Datei lesen** — dort liegen die fertigen
CSS-Variablen, Komponenten-Rezepte und Effekt-Snippets zum Übernehmen.

## Gemeinsame Regeln (gelten für ALLE Themes)

- **Dark-only.** Kein Light-Mode, kein `prefers-color-scheme`-Switch.
- **Tokens statt Hex im Markup:** alle Farben als CSS-Custom-Properties
  (`--bg`, `--panel`, `--fg`, `--muted`, `--accent`, `--ok`, `--warn`, `--err`,
  `--border`) auf `:root` definieren; Komponenten nutzen nur die Variablen.
- **Akzentfarbe ist Bedeutung:** Akzent nur für primäre Aktion + Live/OK-Signale.
  Rot ausschließlich destruktiv/Fehler. Nie Akzent als Deko-Flächenfarbe.
- **Monospace für Daten:** Zahlen, IDs, IPs, Zeiten, Logs immer in der
  Theme-Monofont mit `font-variant-numeric: tabular-nums` (kein Layout-Springen).
- **Keine Emojis als Icons** in neuen UIs — Inline-SVG (Lucide-Style, ein
  Strichgewicht). Statuspunkte als CSS-Dots (`border-radius:50%`), nicht 🟢.
- **Interaktion:** alles Klickbare `cursor:pointer`, sichtbarer `:focus-visible`
  (2px Akzent-Outline), Hover/Press-Übergänge 150–250ms, Touch-Ziele ≥44px.
- **Motion:** Effekte (Glow-Pulse, Glitch, Scanline-Flicker, Typewriter) immer in
  `@media (prefers-reduced-motion: no-preference) { … }` kapseln. Nur
  `transform`/`opacity` animieren.
- **Kontrast:** Fließtext ≥4.5:1 auf Panel-Farbe, Sekundärtext ≥3:1. Neon-Töne
  in Cyberdeck NIE für lange Textblöcke — nur Labels/Werte/Akzente.
- **Layout-Rhythmus:** 4/8px-Spacing-Skala, eine Radius-Stufe pro Theme
  (midnight 10px · cyberdeck 0+Chamfer · phosphor 0), max-width 1100–1200px
  zentriert, mobile-first (die meisten UIs laufen auch auf Toms iPhone).
- **Ein-Datei-Tauglichkeit:** Rezepte sind Vanilla-CSS/HTML (kein Build-Zwang) —
  passend zum Haus-Muster „PAGE-String in FastAPI" (z. B. Jarvis `web.py`);
  in SvelteKit (Portal) dieselben Tokens als `:root`-Block in `+layout`.
- **Fonts:** per Google-Fonts-Import der Theme-Datei; `font-display: swap`.

## Seiten-Grundgerüst (immer gleich)

Header: App-Name links (Theme-Font, dezent) + Status/Uhr rechts in Mono.
Content: Karten/Panels im Grid (`repeat(auto-fill,minmax(320px,1fr))`).
Leerzustand: zentrierter Hinweis + nächste Aktion, nie leere Fläche.
Fehler: Panel mit `--err`-Border links (3px) + Klartext + Retry-Aktion.
