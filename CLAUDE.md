# CLAUDE.md — Tommaso Pacini Digital Works
# Portfolio — Design System & Conventions (v3 — sistema Inter/neutro)

## Panoramica progetto
Portfolio personale di Tommaso Pacini: Data Engineer, Digital Builder, Tech & Design Enthusiast.
Sito: statico HTML/CSS/JS, deploy su **GitHub Pages** (branch `main` → https://tommasopacinii.github.io).
Nessun framework: ogni pagina è un file `.html` self-contained con `<style>` inline.

> NOTA STORICA: il sito nasceva su un design "lavanda + DM Sans/DM Serif". È stato **migrato**
> al sistema Inter/neutro descritto qui sotto. Ignora ogni riferimento residuo a DM Sans / lavanda.

---

## Design System — attuale (v3 Inter / neutro)

### Font (importare sempre)
```html
<link rel="preconnect" href="https://rsms.me/">
<link rel="stylesheet" href="https://rsms.me/inter/inter.css">
<link href="https://fonts.googleapis.com/css2?family=Fragment+Mono&display=swap" rel="stylesheet">
```
- **Display/heading:** `InterDisplay` / `Inter Display` / `Inter`, weight **600** (two-tone: metà soft + metà nera).
- **Body/UI:** `Inter`, weight 400–500.
- **Mono (label/eyebrow/meta):** `Fragment Mono`.

### Token colore (scala neutra) — usati in work/baker/celine
```css
:root{
  --white:#ffffff; --g-50:#fafafa; --g-100:#f7f7f7; --g-150:#f0f0f0; --g-200:#dedede;
  --g-300:#949494;  /* titolo two-tone soft (a11y 3:1) */
  --g-500:#6f6f6f;  /* body/secondario (a11y 4.5:1+) */
  --g-600:#545454; --g-800:#2b2b2b; --black:#000000;
  --green:#21b30b;  /* dot "Available" */
}
```
- `index.html` usa token propri: `--bg:#F0EEE6` (crema), `--text-secondary:#555555`, `--text-muted:#6a6a6a` (a11y).
- Accenti per case study: **ETS** verde `#5aa832`/`Logo.png`; **Baker Hughes** `--bh:#00833f`; **Celine|Gucci** neutro `#1a1a1a`.

### Layout / shell (uguale su tutte le pagine)
- Colonna centrale `.page-frame` (o `.frame`): `max-width:1200px; margin:0 auto; border-left/right:1px solid var(--g-150); background:var(--g-50)`; `body` bianco.
- Sezioni: padding orizzontale **48px** (28px ≤900, 20px ≤560).
- **Nav** sticky identica ovunque: `Home · Work · LinkedIn`, `font-size:13px`, colore `--g-500`, attivo `--black` (solo colore, niente underline), sfondo translucido + blur, `padding:20px 0`.

### Ombre / raggi (dal template launchfolio)
- `--shadow-card`, `--shadow-btn` (bottone nero 3D), `--shadow-float` (pill) — valori esatti nei file.
- Raggi: card 16px, pill 100px, chip 12px.
- Bottoni: `.btn-dark` piatto nero (no gradient/ombra pesante), `.btn-ghost` bordo chiaro.

---

## Accessibilità (regole obbligatorie — apple-design/WCAG AA)
- **Contrasto testo:** ≥ **4.5:1** sotto 17px; ≥ **3:1** per testo ≥18px o bold. (grigi già corretti: body #6f6f6f, soft #949494, index muted #6a6a6a).
- **Focus tastiera:** ogni pagina ha `:focus-visible{ outline:2px solid #1a6dff; outline-offset:3px }` su link/bottoni.
- **Reduced motion:** ogni pagina ha `@media (prefers-reduced-motion: reduce){ * { animation/transition ~0 } }`.
- Info mai affidata al solo colore (es. dot verde + etichetta testuale).
- Controlli icona-only → sempre `aria-label`.

---

## Pagine
| File | Contenuto |
|---|---|
| `index.html` | Home/About (sfondo crema, hero + stats + Experience + toolkit) |
| `work.html` | **Work** principale: hero stack, marquee loghi, griglia progetti, services, about (facets), contatto mobile-first |
| `ets-case-study.html` | Case study **ETS** (in inglese): hero two-tone, process bar, UX/Figma/Vibe coding/Workflow, terminale, CTA |
| `baker-hughes.html` | Esperienza Baker Hughes (Project Controls & Cost Analyst) — timeline, highlights, responsibilities |
| `celine-gucci.html` | Esperienza Celine & Gucci (BI & Data Analysis) — due blocchi brand con periodi |
| `images/` · `files/` | Loghi, screenshot, avatar, `files/Tommaso-Pacini-CV.pdf` |

Le card in `work.html` linkano alle rispettive pagine; ogni case study ha "← Back to work".

---

## Convenzioni codice / asset
- **Nomi file web-safe:** minuscolo, niente spazi (GitHub Pages è **case-sensitive**: `celine.png` ≠ `Celine.png`; gli spazi danno 404). Loghi tool in `images/Logos/`.
- Placeholder immagini: commento `<!-- REPLACE: ... -->` + spesso `onerror` di fallback.
- Mobile-first: nessuno scroll orizzontale, tap target adeguati, stack decorativi nascosti su ≤640px dove serve.
- Le etichette "//" in stile commento NON vanno mostrate a schermo (sono commenti di codice, non UI).

## Deploy
- `git add <file portfolio>` → **mai** `git add .` (esclude `.claude/`, `awesome-design/`).
- Commit + `git push origin main` → GitHub Pages aggiorna in ~1 min (Ctrl+F5 per cache).
- Se il remote è avanti (upload web), `git merge -X ours --no-edit origin/main` prima del push.
- **NON committare** file sensibili/personali (es. firma digitale) → sarebbero pubblici.

## Regole Claude — errori da non ripetere
- USARE **Inter / Inter Display / Fragment Mono** (NON DM Sans/DM Serif, NON reintrodurre il lavanda).
- Titoli display **Inter Display 600**, two-tone (soft `--g-300` + hard `--black`).
- Rispettare i contrasti a11y sopra; non schiarire i grigi sotto le soglie.
- Nav e shell (page-frame 1200 + bordi) **identici** su tutte le pagine.
- Bottoni minimal (niente ombre 3D pesanti fuori dai token definiti).

## Link utili
- LinkedIn: https://www.linkedin.com/in/tommaso-pacini-035a2924a/
- Email: tommasoopacinii@gmail.com
- ETS (sito reale, progetto separato): https://www.etswind.com
