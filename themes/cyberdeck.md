# Theme „cyberdeck" — Neon-HUD (auffällig)

Charakter: Sci-Fi-Deck. Void-Schwarz, Neon-Dreiklang (Grün primär, Magenta/Cyan
sekundär), Chamfer-Ecken, HUD-Brackets, subtiler Glitch. Für Status-Walls,
Show-Oberflächen, verspielte Tools. NICHT für lange Lese-/Formularstrecken.

## Tokens

```css
@import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@500;700&family=JetBrains+Mono:wght@400;500&display=swap');
:root{
  --bg:#0A0A0F; --panel:#12121A; --panel-2:#1C1C2E; --border:#2A2A3A;
  --fg:#E0E0E0; --muted:#8B8B9E;
  --accent:#00FF88; --accent2:#FF00FF; --accent3:#00D4FF; --err:#FF3366;
  --radius:0; --font:'JetBrains Mono',monospace; --head:'Orbitron',sans-serif;
}
body{margin:0;background:var(--bg);color:var(--fg);font:14px/1.5 var(--font)}
h1,h2{font-family:var(--head);letter-spacing:.12em;text-transform:uppercase}
```

## Signature-Effekte

```css
/* Chamfer-Ecken (45°) statt border-radius */
.panel{background:var(--panel);border:1px solid var(--border);padding:16px;
  clip-path:polygon(12px 0,100% 0,100% calc(100% - 12px),calc(100% - 12px) 100%,0 100%,0 12px)}

/* HUD-Eckklammern um wichtige Panels */
.hud{position:relative}
.hud::before,.hud::after{content:"";position:absolute;width:14px;height:14px;pointer-events:none}
.hud::before{top:-1px;left:-1px;border-top:2px solid var(--accent);border-left:2px solid var(--accent)}
.hud::after{bottom:-1px;right:-1px;border-bottom:2px solid var(--accent);border-right:2px solid var(--accent)}

/* Neon-Button mit Glow */
.btn{font:600 13px var(--font);letter-spacing:.1em;text-transform:uppercase;cursor:pointer;
  background:transparent;color:var(--accent);border:1px solid var(--accent);padding:10px 18px;
  clip-path:polygon(8px 0,100% 0,100% calc(100% - 8px),calc(100% - 8px) 100%,0 100%,0 8px);
  transition:all .15s}
.btn:hover{background:var(--accent);color:#04120A;box-shadow:0 0 18px rgb(0 255 136/.45)}
.btn.alt{color:var(--accent3);border-color:var(--accent3)}
.btn.alt:hover{background:var(--accent3);color:#03121A;box-shadow:0 0 18px rgb(0 212 255/.45)}
:focus-visible{outline:2px solid var(--accent);outline-offset:2px}

/* Scanlines (dezent!) + Glitch nur auf Aktiv-Elementen */
@media (prefers-reduced-motion:no-preference){
  body::before{content:"";position:fixed;inset:0;pointer-events:none;z-index:9999;opacity:.05;
    background:repeating-linear-gradient(0deg,transparent 0 2px,#000 2px 3px)}
  .glitch:active{animation:glitch .25s steps(2) both}
  @keyframes glitch{25%{transform:translateX(2px)}75%{transform:translateX(-2px)}}
}

/* Neon-Text (nur Überschriften/Hero-Werte, NIE Fließtext) */
.neon{color:var(--accent);text-shadow:0 0 6px rgb(0 255 136/.6),0 0 20px rgb(0 255 136/.25)}
.neon.m{color:var(--accent2);text-shadow:0 0 6px rgb(255 0 255/.6)}
```

## Do / Don't

- Do: Farb-Rollen fest — Grün=primär/OK, Cyan=Info/Sekundäraktion,
  Magenta=Highlights/Deko-Akzent, `--err`=Fehler. Fließtext bleibt `--fg` grau.
- Do: Chamfer konsequent (clip-path), `--radius` bleibt 0.
- Don't: mehr als 1 Glitch-Element pro View; Scanlines >6% Opacity;
  Neon-Glow auf Textblöcken; Orbitron für Fließtext (nur Headlines).
