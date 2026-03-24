# findr-web — Project Memory

## Project Status

- **State**: Live single-page landing site, fully functional
- **Version**: v1.0 — initial launch build
- **Git**: Not initialized yet
- **Build system**: None — single self-contained HTML file, no dependencies
- **Last updated**: 2026-03-24

---

## File Structure

```
findr-web/
  index.html   — Entire site: HTML + CSS + JS + i18n (~177KB, 331 lines)
  SKILL.md     — Full design system documentation
  MEMORY.md    — This file (project memory for future sessions)
```

Everything lives in `index.html`:
- **Lines 8–100**: All CSS (inline `<style>` block)
- **Lines 102–195**: All HTML structure
- **Lines 196–197**: i18n translations (`window.__TR`) and ticker data (`window.__TICKER`) — massive inline JSON objects for EN/LV/RU
- **Lines 198–329**: All JavaScript (theme toggle, i18n, scroll reveal, FAQ accordion, flow canvas animation, TV noise canvas)

---

## Design System Summary

### Colors (CSS Custom Properties)

| Token      | Light     | Dark      | Role                    |
|-----------|-----------|-----------|-------------------------|
| `--bg`    | `#ffffff` | `#080808` | Page background         |
| `--fg`    | `#0a0a0a` | `#f0f0f0` | Primary text            |
| `--accent`| `#ff4500` | `#ff4500` | Brand accent (fixed)    |
| `--muted` | `#999`    | `#555`    | Secondary/description   |
| `--border`| `#e0e0e0` | `#1e1e1e` | Borders, grid gaps      |
| `--card`  | `#f5f5f5` | `#111`    | Card/hover backgrounds  |

### Fonts

- **Space Mono** (400, 700) — all headings, labels, buttons, nav, UI elements
- **DM Sans** (300, 400, 500) — body paragraphs, descriptions, FAQ answers
- Loaded via Google Fonts CDN

### Layout

- Max content width: **860px**, centered
- Fixed nav bar at top (z-index 100)
- `main` has `padding-top: 80px` to clear nav
- Sections use `.section` class: `max-width: 860px; padding: 48px 24px; border-top: 1px solid var(--border)`
- Card grids use 1px-gap technique (grid gap `1px`, background `var(--border)`, items background `var(--bg)`)

### Responsive Breakpoints

| Breakpoint | Changes |
|-----------|---------|
| <= 700px  | Nav padding shrinks, social links hidden, flow canvas 420px tall, sections 32px/16px, grids 2-col, footer stacked, CTA column-reverse |
| <= 400px  | Steps and tasks grids become single column |

---

## Sections Documented

### 1. Navigation (fixed)
- **Logo**: "findr" (Space Mono, 22px, bold)
- **Right side**: Social links (X/Twitter, Telegram) → Language switcher (EN/LV/RU) → Theme toggle button
- Social links hidden on mobile (<= 700px)

### 2. Hero Section
- Full viewport height, centered
- **Tag**: "AI HUMAN SOLUTION" (accent, 10px, 3px spacing)
- **Name**: "findr" (Space Mono, clamp 52–96px, bold, -4px tracking)
- **Subtitle**: DM Sans, clamp 15–18px, muted, max-width 460px
- **CTA button**: "SEND YOUR TASK" → links to https://t.me/gtfindr
- **Flow Canvas**: animated diagram below CTA
- All elements stagger-animate in with `fadeUp` (0.2s–0.9s delays)

### 3. Flow Canvas (`#flowCanvas`)
- HTML5 Canvas with continuous animation (requestAnimationFrame)
- Shows input labels → bezier curves with glowing dots → central "findr" circle → curves → output labels
- Desktop: horizontal (inputs left, outputs right)
- Mobile: vertical (inputs top, outputs bottom)
- Labels are language-aware (change with i18n switcher)
- Central node has pulsing glow ring

### 4. Ticker
- Infinite horizontal scroll (22s linear, CSS animation)
- Items separated by accent `*` dots
- Border top/bottom, card background
- Content rebuilt dynamically per language from `window.__TICKER`

### 5. How It Works (`.section.reveal`)
- Label: "HOW IT WORKS"
- Heading: "simple as sending a message"
- 4-step grid (`repeat(auto-fit, minmax(180px, 1fr))`):
  - 01: send your task
  - 02: i confirm the price
  - 03: i do the work
  - 04: you get the answer
- 1px-gap grid technique, hover to `--card` background

### 6. What You Can Send (`.section.reveal`)
- Label: "WHAT YOU CAN SEND"
- Heading: "if it takes your time, send it to me"
- 12 task examples in grid (`repeat(auto-fit, minmax(230px, 1fr))`):
  - Cyber protection, logo, research, crypto project, AI tool selection, service comparison, website, social media setup, idea evaluation, automation, tool finding, general help
- Monospace text, hover reveals full color

### 7. FAQ (`.section.reveal`)
- Label: "FAQ"
- Heading: "questions answered simply"
- 6 accordion items (only one open at a time):
  - What exactly is findr
  - How much does it cost
  - Is my information safe
  - How do I know if findr can help
  - How fast will I get a response
  - Do I need to know anything about AI
- Toggle: `+` icon rotates 45deg, answer slides open via `max-height` transition

### 8. CTA Section (`.section.reveal`)
- Flex layout: text left, TV canvas right
- Eyebrow: "READY?"
- Headline: "stop wasting your time."
- Subtitle: "Send your task. Get a price. Get it done."
- CTA button: "SEND ME A MESSAGE" with Telegram SVG icon → https://t.me/gtfindr
  - Accent background, white text, shine-on-hover, lift effect with shadow
- **TV Canvas** (`#tvCanvas`): 220x220 static noise effect with overlaid hidden image, scanlines, vignette, random glitch

### 9. Footer
- Three-part flex: logo, social links (X + Telegram), copyright "2026 FINDR"
- Max-width 860px centered
- Mobile: stacked column, centered

---

## Interactive Features

| Feature          | Mechanism                                  | Persists?              |
|------------------|--------------------------------------------|------------------------|
| Theme toggle     | `data-theme` attr on `<body>`, button text | No (resets on reload)  |
| Language (i18n)  | `data-i18n` attrs + `window.__TR` lookup   | Yes (`localStorage`)   |
| Scroll reveal    | `IntersectionObserver` at 0.08 threshold   | N/A                    |
| FAQ accordion    | `toggleFaq()` — max-height + class toggle  | N/A                    |
| Flow animation   | Canvas rAF loop with bezier LUT sampling   | N/A                    |
| TV noise         | Canvas rAF loop with pixel noise + glitch  | N/A                    |

---

## External Links

| Label              | URL                        | Where used        |
|--------------------|----------------------------|--------------------|
| Telegram DM (CTA)  | https://t.me/gtfindr       | Hero CTA, CTA btn |
| X / Twitter         | https://x.com/findrdesk    | Nav, footer        |
| Telegram channel    | https://t.me/findrdesk     | Nav, footer        |

---

## GSD Rules for Future Sessions

### Architecture Rules
1. **Single-file structure** — do not split into separate CSS/JS files unless explicitly migrating to a build system
2. **No frameworks** — no Tailwind, Bootstrap, React, or build tools. Pure HTML/CSS/JS
3. **No external dependencies** beyond Google Fonts CDN
4. **CSS custom properties only** — never use hardcoded colors; always reference `var(--token)`

### Design Rules
5. **Accent `#ff4500` is sacred** — never change it, never theme-vary it
6. **Space Mono for UI, DM Sans for body** — never swap these roles
7. **860px max-width** for all content sections
8. **1px-gap grid technique** for all card/grid layouts (border background, item background)

### i18n Rules
9. **All user-facing text must have `data-i18n` attribute**
10. **All three languages required** — EN, LV, RU translations in `window.__TR`
11. **Ticker items** go in `window.__TICKER` for all three languages
12. **Flow canvas labels** — update `FLOW_INPUTS`, `FLOW_INPUTS_MOB`, `FLOW_OUTPUTS`, `FLOW_OUTPUTS_MOB` if changing canvas text

### New Section Checklist
13. Wrap in `<div class="section reveal">`
14. Add `.section-label` with `data-i18n`
15. Add `<h2>` with `data-i18n`
16. Add `data-i18n` to all text content
17. Add all translations to `window.__TR` (EN/LV/RU)
18. Test light theme + dark theme
19. Test at desktop, 700px, and 400px breakpoints
20. Verify scroll reveal triggers properly

### Quality Gates
21. **Both themes** must look correct before any change is considered done
22. **All three languages** must be tested
23. **Mobile layout** must not break (test 700px and 400px)
24. **Canvas animations** must still run smoothly after changes
25. **No new external requests** — keep the site self-contained (except Google Fonts)

### Session Resumption
- Read this file first to restore full context
- Read SKILL.md for detailed design token values and component specs
- The entire site is in `index.html` — read it in chunks (331 lines but ~177KB due to inline translation JSON on lines 196–197)
- Lines 196–197 contain the bulk of the file size (translation objects) — skip unless modifying translations
