# Theme „phosphor" — Amber-CRT-Retro

Charakter: alter Bernstein-Phosphor-Monitor. Mono-Amber auf Fast-Schwarz,
Bloom-Glow, Scanlines, Dotted-Leader-Statuszeilen. Für CLI-artige Tools,
Log-Viewer, Diagnose-/Einzweck-Seiten. Ein-Farben-Welt: Amber trägt alles,
Grün/Rot sind ausschließlich Statuspunkte.

## Tokens

```css
@import url('https://fonts.googleapis.com/css2?family=Space+Mono:wght@400;700&display=swap');
:root{
  --bg:#0A0806; --panel:#12100C; --border:#3A2E10;
  --fg:#FFB000; --dim:#B37E00; --faint:#7A5800;
  --ok:#4AF626; --err:#FF4444;
  --radius:0; --mono:'Space Mono',monospace;
}
body{margin:0;background:var(--bg);color:var(--fg);font:14px/1.5 var(--mono)}
```

## Signature-Effekte

```css
/* Bloom: genereller weicher Glow auf allem Text (das CRT-Gefühl) */
body{text-shadow:0 0 8px rgb(255 176 0 / .3)}

/* Scanlines + Vignette (keine Curvature — bleibt lesbar) */
@media (prefers-reduced-motion:no-preference){
  body::before{content:"";position:fixed;inset:0;pointer-events:none;z-index:9999;opacity:.06;
    background:repeating-linear-gradient(0deg,transparent 0 2px,#000 2px 3px)}
}
body::after{content:"";position:fixed;inset:0;pointer-events:none;z-index:9998;
  background:radial-gradient(ellipse at center,transparent 60%,rgb(0 0 0/.35) 100%)}

/* Panel im TTY-Stil */
.panel{background:var(--panel);border:1px solid var(--border);padding:14px 16px}
.panel h2{margin:0 0 10px;font-size:14px;font-weight:700;letter-spacing:.1em;
  text-transform:uppercase;border-bottom:1px solid var(--border);padding-bottom:8px}

/* Dotted-Leader-Statuszeile:  name ......... [ OK ] */
.row{display:flex;align-items:baseline;gap:8px}
.row .leader{flex:1;border-bottom:1px dotted var(--faint);transform:translateY(-4px)}
.row .st{font-weight:700}
.st.ok{color:var(--ok);text-shadow:0 0 8px rgb(74 246 38/.4)}
.st.err{color:var(--err);text-shadow:0 0 8px rgb(255 68 68/.4)}

/* Prompt + blinkender Block-Cursor */
.prompt::before{content:"> ";color:var(--dim)}
@media (prefers-reduced-motion:no-preference){
  .cursor::after{content:"▊";animation:blink 1s steps(1) infinite}
  @keyframes blink{50%{opacity:0}}
}

/* Button als Klammer-Kommando, Invert bei Hover */
.btn{font:700 13px var(--mono);cursor:pointer;background:transparent;color:var(--fg);
  border:1px solid var(--fg);padding:8px 14px;text-transform:uppercase;letter-spacing:.06em;
  transition:all .12s}
.btn::before{content:"[ "} .btn::after{content:" ]"}
.btn:hover{background:var(--fg);color:var(--bg);text-shadow:none}
:focus-visible{outline:2px solid var(--fg);outline-offset:2px}
```

## Do / Don't

- Do: alles in Amber-Abstufungen (`--fg`/`--dim`/`--faint`) denken; Hierarchie
  über Helligkeit, nicht über andere Farbtöne.
- Do: Uppercase-Titel, Dotted-Leader für Status, Prompt-Ästhetik für Eingaben.
- Don't: zweite Akzentfarbe einführen; border-radius; Sans-Serif-Fonts;
  Bloom über .4 Opacity (wird matschig); Curvature-/Fisheye-Effekte.
