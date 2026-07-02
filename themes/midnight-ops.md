# Theme „midnight-ops" — professionelles Ops-Dark (Default)

Charakter: ruhige NASA-Konsole, nicht Matrix. Slate-Deep-Blue, ein Run-Green-Akzent,
hohe Lesbarkeit (WCAG AAA-tauglich), dezenter Glow. Für Dashboards/Admin/Portale.

## Tokens

```css
@import url('https://fonts.googleapis.com/css2?family=IBM+Plex+Sans:wght@400;500;600&family=JetBrains+Mono:wght@400;500&display=swap');
:root{
  --bg:#0F172A; --panel:#1E293B; --panel-2:#172033; --border:#334155;
  --fg:#F8FAFC; --muted:#94A3B8; --faint:#64748B;
  --accent:#22C55E; --accent-dim:#15803D;
  --ok:#22C55E; --warn:#F59E0B; --err:#EF4444; --info:#38BDF8;
  --radius:10px; --font:'IBM Plex Sans',system-ui,sans-serif;
  --mono:'JetBrains Mono',monospace;
}
body{margin:0;background:var(--bg);color:var(--fg);font:15px/1.55 var(--font)}
```

## Komponenten-Rezepte

```css
/* Karte */
.card{background:var(--panel);border:1px solid var(--border);border-radius:var(--radius);
  padding:16px;transition:border-color .2s}
.card:hover{border-color:#475569}

/* Primär-Button (Run-Green) + Sekundär + Danger */
.btn{font:600 14px var(--font);border:0;border-radius:8px;padding:10px 16px;cursor:pointer;
  background:var(--accent);color:#052E16;transition:filter .15s,transform .1s}
.btn:hover{filter:brightness(1.1)} .btn:active{transform:scale(.98)}
.btn.sec{background:transparent;color:var(--fg);border:1px solid var(--border)}
.btn.danger{background:transparent;color:var(--err);border:1px solid var(--err)}
:focus-visible{outline:2px solid var(--accent);outline-offset:2px}

/* Status-Dot mit sanftem Puls (nur live/ok pulsiert) */
.dot{display:inline-block;width:8px;height:8px;border-radius:50%;background:var(--ok)}
.dot.warn{background:var(--warn)} .dot.err{background:var(--err)}
@media (prefers-reduced-motion:no-preference){
  .dot.live{animation:pulse 2.4s ease-in-out infinite}
  @keyframes pulse{50%{box-shadow:0 0 0 5px rgb(34 197 94 / .15)}}
}

/* Daten/Metriken: Mono + tabular */
.metric{font:500 22px/1.2 var(--mono);font-variant-numeric:tabular-nums}
.label{font:11px/1 var(--font);letter-spacing:.08em;text-transform:uppercase;color:var(--muted)}

/* Tabelle */
table{border-collapse:collapse;width:100%}
th{font:600 11px var(--font);letter-spacing:.08em;text-transform:uppercase;color:var(--muted);
  text-align:left;padding:8px 12px;border-bottom:1px solid var(--border)}
td{padding:10px 12px;border-bottom:1px solid var(--panel-2);font-family:var(--mono);font-size:13px}
tr:hover td{background:var(--panel-2)}

/* Badge */
.badge{font:600 11px var(--mono);padding:3px 8px;border-radius:999px;border:1px solid}
.badge.ok{color:var(--ok);border-color:var(--accent-dim)}
.badge.err{color:var(--err);border-color:#7F1D1D}
```

## Do / Don't

- Do: viel Fläche `--bg`, Karten `--panel`, Hierarchie über Border+Spacing.
- Do: Glow höchstens `text-shadow:0 0 10px` auf einer Hero-Zahl.
- Don't: mehrere Akzentfarben gleichzeitig; Grün als Flächen-Hintergrund;
  Neon-Effekte, Scanlines, Glitch (das gehört zu cyberdeck).
