# hacker-ui — Toms dunkles Ops-Designsystem

Claude-Code-**Skill** + Designsystem für alle selbstgebauten Web-UIs im Homelab
(Jarvis-Feed, Service-Portal, Status-/Admin-Seiten, neue Apps). Dunkel,
technisch, akzentfarben-getrieben — drei Themes, eine Regelbasis.

## Themes

| Theme | Charakter | Einsatz |
|---|---|---|
| [`midnight-ops`](themes/midnight-ops.md) | Slate-Blau + Run-Green, ruhig, WCAG AAA | **Default** — Dashboards, Admin, Portale |
| [`cyberdeck`](themes/cyberdeck.md) | Void-Schwarz + Neon-Dreiklang, Chamfer, HUD | Show-Oberflächen, Status-Walls |
| [`phosphor`](themes/phosphor.md) | Amber-CRT, Bloom, Scanlines, TTY | CLI-Tools, Log-Viewer, Diagnose |

Demos: `demos/<theme>.html` im Browser öffnen (kein Build nötig).

## Nutzung als Claude-Code-Skill

```bash
git clone git@github.com:gnoffer/hacker-ui.git ~/hacker-ui
ln -s ~/hacker-ui ~/.claude/skills/hacker-ui
```

Danach greift der Skill automatisch bei UI-Arbeit („baue die Seite im
cyberdeck-Theme") — [SKILL.md](SKILL.md) enthält die Entscheidungsregeln,
die Theme-Dateien die fertigen CSS-Tokens und Komponenten-Rezepte.

## Prinzipien (Kurzfassung)

- Dark-only, ein Theme pro App, Tokens statt roher Hex-Werte.
- Akzentfarbe = Bedeutung (primäre Aktion/OK) — Rot nur destruktiv.
- Monospace + `tabular-nums` für alle Daten; SVG-Icons statt Emojis.
- Effekte (Glow/Glitch/Scanlines) immer hinter `prefers-reduced-motion`.
- Vanilla-CSS/HTML — passt zum Haus-Muster „PAGE-String in FastAPI" und SvelteKit.
