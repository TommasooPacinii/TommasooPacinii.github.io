# CLAUDE.md — Tommaso Pacini Digital Works
# Portfolio Framer — Design System & Conventions (v2 — nuovo design lavanda)

## Panoramica progetto
Portfolio personale di Tommaso Pacini: Data Engineer, Digital Builder, Tech & Design Enthusiast.
Sito live attuale: https://tommasopacindigital.framer.website
Stack: Framer (visual builder) + override React/TypeScript per logica custom + HTML/CSS standalone per pagine extra.

---

## ATTENZIONE — Migrazione design in corso
Il sito sta migrando dal design monocromatico originale (bianco/nero) a un nuovo design
con sfondo lavanda, accenti viola, tipografia mista (DM Sans + DM Serif Display).
Tutte le nuove pagine usano il NUOVO design system qui sotto.

---

## Design System — NUOVO (v2 lavanda)

### CSS Variables (da usare sempre)
```css
:root {
  --bg: #ECEAF4;                /* sfondo pagina principale */
  --bg-card: #ffffff;           /* sfondo card e pannelli */
  --bg-dark: #14122A;           /* sfondo sezioni scure (hero CS, footer) */
  --bg-surface: #E4E2EE;        /* sfondo elementi interni, placeholder */
  --purple: #7B6EE8;            /* viola principale, CTA, link */
  --purple-light: #EEEDFE;      /* sfondo tag UX, hover leggero */
  --purple-mid: #AFA9EC;        /* testo secondario viola, badge dark */
  --purple-dark: #3C3489;       /* hover su purple, testo su purple-light */
  --text-primary: #14122A;      /* titoli, testo principale */
  --text-secondary: #6B6880;    /* corpo testo, descrizioni */
  --text-muted: #9896A8;        /* label, meta info, placeholder */
  --border: #D6D4E8;            /* bordi card e divisori */
  --font-display: 'DM Serif Display', serif;
  --font-body: 'DM Sans', sans-serif;
  --radius-card: 20px;
  --radius-pill: 100px;
  --radius-sm: 8px;
  --transition: 0.25s cubic-bezier(0.4, 0, 0.2, 1);
}
```

### Font Google da importare sempre
```html
<link href="https://fonts.googleapis.com/css2?family=DM+Sans:opsz,wght@9..40,300;9..40,400;9..40,500&family=DM+Serif+Display:ital@0;1&display=swap" rel="stylesheet">
```

### Palette tag/badge per categoria
```
UX/Design:   background #EEEDFE, color #3C3489  (tag-ux)
Data/BI:     background #E1F5EE, color #0F6E56  (tag-data)
Web/Brand:   background #FAECE7, color #993C1D  (tag-web)
VR/Tech:     background #E6F1FB, color #185FA5  (tag-vr)
Neutral:     background #F1EFE8, color #5F5E5A  (tag-neutral)
```

### Tipografia
```
Display/Hero:    DM Serif Display, italic, ~32–48px
H1 pagina:       DM Sans, weight 400, ~22–32px, colore text-secondary
H2 sezione:      DM Sans, weight 500, ~20px, colore text-primary
H3 sottosezione: DM Sans, weight 500, ~16–18px
Body:            DM Sans, weight 400, 14px, line-height 1.7, text-secondary
Label/Meta:      DM Sans, weight 400, 10–11px, uppercase, letter-spacing 0.1em, text-muted
```

**Regola:** Solo weight 300, 400, 500. Mai 600 o 700.

---

## Struttura pagine

### Home (/) — da migrare al nuovo design
- Hero: testo sinistra, elemento 3D dorato/viola destra
- Sfondo: #ECEAF4
- CTA "Tell me more ↗" con stile bottone dark arrotondato

### Work (/work.html) — COMPLETATA
- File: `work.html`
- Griglia progetti: card in lista verticale (300px img + corpo testo)
- Filtri categoria in top
- Case study ETS inline nella stessa pagina
- Footer scuro #14122A

### Case study ETS — struttura
```
1. Hero dark (#14122A) — titolo serif, tag, sottotitolo
2. Meta grid (4 colonne): Role, Duration, Tools, Type
3. 01 Overview
4. 02 Challenge
5. 03 Process (steps numerati)
6. 04 Outcomes (3 stat card con numero grande serif)
7. 05 Gallery (griglia 2x2)
8. Footer: nota + "Next project →"
```

### Sezioni da sviluppare
- [ ] Pagina About separata
- [ ] Case study: Project 2 (placeholder)
- [ ] Case study: VR Wander study
- [ ] Chat AI + form contatto con invio email (Resend API)

---

## Componenti chiave

### Card progetto
```css
grid-template-columns: 300px 1fr;
border-radius: 20px;
border: 1px solid var(--border);
hover: translateY(-3px) + box-shadow rgba(123,110,232,0.1)
```

### Tag badge
```css
font-size: 10px; font-weight: 500;
padding: 4px 11px; border-radius: 100px;
text-transform: uppercase; letter-spacing: 0.04em;
```

### Bottone CTA viola
```css
color: var(--purple); background: none; border: none;
transition: gap 0.25s; /* gap aumenta su hover */
```

### Outcome card (stat)
```css
background: var(--bg-surface); border-radius: 14px; padding: 24px 20px;
numero: DM Serif Display, 40px, color var(--purple)
label: 12px, text-secondary
```

### Nav sticky
```css
background: rgba(236,234,244,0.85); backdrop-filter: blur(12px);
font-size: 13px; gap: 36px;
active: border-bottom 1.5px solid var(--text-primary)
```

---

## Convenzioni codice

### Animazioni entry
Ogni sezione entra con fadeUp:
```css
@keyframes fadeUp { to { opacity: 1; transform: translateY(0); } }
elemento: opacity: 0; transform: translateY(16px); animation: fadeUp 0.6s ease forwards;
/* usa animation-delay per staggering: 0.1s, 0.2s, 0.3s */
```

### Immagini nei placeholder
Ogni placeholder ha un commento `<!-- REPLACE: ... -->` che indica esattamente quale immagine inserire.
Formato consigliato: JPG o WebP, ottimizzate, max 800px larghezza per card cover.

### Framer Override (quando applicabile)
```typescript
import { ComponentType } from "react"
import { Override } from "framer"

export function NomeComponente(): Override {
  return {
    style: {
      fontFamily: "'DM Sans', sans-serif",
      // usa sempre le variabili CSS del design system
    }
  }
}
```

---

## Integrazioni pianificate

### Email / Chat AI (Fase 2)
- Provider email: Resend (https://resend.com) — semplice, API moderna
- Trigger: form di contatto nella pagina Work o nella home
- Flow: utente invia → email a tommasoopacinii@gmail.com + risposta automatica all'utente
- AI feature futura: risposta personalizzata generata con Claude API

### CMS contenuti (opzionale)
- Framer CMS per gestire i progetti senza toccare il codice
- Alternativa: JSON statico per i contenuti dei case study

---

## Regole Claude — Errori da non ripetere

- NON usare Inter, Roboto, Arial, Space Grotesk — usare DM Sans + DM Serif Display
- NON usare sfondo bianco puro come bg pagina — usare #ECEAF4
- NON usare font-weight > 500
- NON aggiungere ombre decorative pesanti — solo box-shadow leggero su hover card
- NON usare colori accentuati fuori dalla palette viola (no rossi, verdi brillanti)
- I tag categoria hanno sempre colori specifici per tipo (vedi palette tag sopra)
- Le sezioni label hanno sempre il trattino decorativo ::before (width 24px, height 1px)
- Il case study hero è sempre su sfondo #14122A (dark), non viola

---

## File prodotti
- `work.html` — pagina Work completa con card e case study ETS
- `CLAUDE.md` — questo file

## Link utili
- Sito live: https://tommasopacindigital.framer.website
- LinkedIn: https://www.linkedin.com/in/tommaso-pacini-035a2924a/
- Email: tommasoopacinii@gmail.com
- Figma Work page: https://www.figma.com/design/B43vkljjn52UWc19pWfMkB/
- Font: https://fonts.google.com/specimen/DM+Sans
