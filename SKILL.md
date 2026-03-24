# findr — Design System & Development Guide

## Brand Identity

- **Name**: findr (always lowercase)
- **Tagline**: AI HUMAN SOLUTION
- **Positioning**: A human intermediary who uses AI tools to solve client problems — "a smart friend who actually knows this stuff"
- **Year**: 2026

---

## Color System

All colors use CSS custom properties on `:root` / `[data-theme="dark"]`.

| Token        | Light           | Dark            | Usage                              |
|-------------|-----------------|-----------------|-------------------------------------|
| `--bg`      | `#ffffff`       | `#080808`       | Page background                     |
| `--fg`      | `#0a0a0a`       | `#f0f0f0`       | Primary text                        |
| `--accent`  | `#ff4500`       | `#ff4500`       | Brand accent (same both themes)     |
| `--muted`   | `#999`          | `#555`          | Secondary text, descriptions        |
| `--border`  | `#e0e0e0`       | `#1e1e1e`       | Borders, grid gaps                  |
| `--card`    | `#f5f5f5`       | `#111`          | Card/hover backgrounds              |

**Key rule**: `--accent` (#ff4500, orangered) is identical in both themes. Never change it per-theme.

---

## Typography

### Font Stack
- **Headings / UI / Mono elements**: `'Space Mono', monospace` — weights 400, 700
- **Body text**: `'DM Sans', sans-serif` — weights 300, 400, 500
- **Google Fonts import**: `Space+Mono:wght@400;700&family=DM+Sans:wght@300;400;500`

### Type Scale

| Element           | Font             | Size                         | Weight | Letter-spacing | Notes                |
|-------------------|------------------|------------------------------|--------|----------------|----------------------|
| Hero name         | Space Mono       | `clamp(52px, 9vw, 96px)`    | 700    | -4px           | Tight tracking       |
| Section h2        | Space Mono       | `clamp(22px, 3.5vw, 36px)`  | 700    | -1.5px         |                      |
| CTA headline      | Space Mono       | `clamp(20px, 2.8vw, 34px)`  | 700    | -1.5px         | `white-space:nowrap` |
| Nav logo          | Space Mono       | 22px                         | 700    | -1px           |                      |
| Footer logo       | Space Mono       | 16px                         | 700    | -1px           |                      |
| Section label     | Space Mono       | 10px                         | 400    | 3px            | Accent color         |
| CTA eyebrow       | Space Mono       | 10px                         | 400    | 4px            | Accent color         |
| Step number        | Space Mono       | 10px                         | 400    | 2px            | Accent color         |
| Step heading       | Space Mono       | 13px                         | 700    | -0.3px         |                      |
| FAQ question       | Space Mono       | 13px                         | 700    | -0.3px         |                      |
| Body paragraph     | DM Sans          | 15px                         | 300    | default        | Line-height 1.8      |
| Hero subtitle      | DM Sans          | `clamp(15px, 2vw, 18px)`    | 300    | default        | Line-height 1.7      |
| Task item          | Space Mono       | 11px                         | 400    | default        | Muted color          |
| Theme button       | Space Mono       | 11px                         | 400    | 1px            |                      |
| Nav social links   | Space Mono       | 11px                         | 400    | 1px            |                      |
| Lang button        | Space Mono       | 10px                         | 400    | 1px            |                      |
| Ticker item        | Space Mono       | 10px                         | 400    | 2px            |                      |
| Footer socials     | Space Mono       | 10px                         | 400    | 2px            |                      |
| Footer copy        | Space Mono       | 10px                         | 400    | 1px            |                      |
| FAQ answer         | DM Sans          | 14px                         | 400    | default        | Line-height 1.8      |
| CTA sub            | DM Sans          | 14px                         | 400    | default        | Line-height 1.7      |

**Pattern**: Space Mono is used for ALL UI elements, labels, buttons, headings. DM Sans is only for body/paragraph text.

---

## Layout System

### Global
- Max content width: **860px** (centered with `margin: 0 auto`)
- No CSS framework — pure custom CSS with CSS custom properties
- `box-sizing: border-box` on all elements
- `scroll-behavior: smooth` on html
- `overflow-x: hidden` on body
- All transitions: `.2s` to `.4s` duration

### Navigation
- Fixed top (`position: fixed; z-index: 100`)
- Flex layout: logo left, controls right
- Padding: `20px 40px` (desktop), `14px 20px` (mobile)
- Bottom border: `1px solid var(--border)`
- Background matches `--bg` with transition

### Sections
- Class: `.section`
- Padding: `48px 24px` (desktop), `32px 16px` (mobile)
- Top border: `1px solid var(--border)`
- Max-width: 860px centered

### Content padding
- `main` has `padding-top: 80px` to clear fixed nav

---

## Component Catalog

### Hero Section (`.hero`)
- Full viewport height (`min-height: 100vh`)
- Centered flex column
- Contains: tag line, brand name, subtitle, CTA button, flow canvas
- All elements animate in with staggered `fadeUp` animation (0.2s–0.9s delays)

### Flow Canvas (`#flowCanvas`)
- Animated HTML5 Canvas showing inputs flowing into central "findr" node and outputs flowing out
- Desktop: horizontal layout (inputs left, outputs right)
- Mobile: vertical layout (inputs top, outputs bottom)
- Quadratic bezier curves with animated glowing dots
- Central node: circle with pulsing ring, "findr" text inside
- Colors adapt to theme

### Ticker
- Infinite horizontal scroll animation (`22s linear infinite`)
- Items separated by accent-colored `*` dots
- Border top and bottom, card background
- Content is language-aware (built dynamically)

### Steps Grid (`.steps`)
- CSS Grid: `repeat(auto-fit, minmax(180px, 1fr))`
- 1px gap with border-colored background (creates grid lines)
- Each step: number (accent), heading, description
- Hover: background changes to `--card`
- Mobile: 2 columns, then 1 column at 400px

### Tasks Grid (`.tasks-grid`)
- CSS Grid: `repeat(auto-fit, minmax(230px, 1fr))`
- Same 1px-gap border technique as steps
- Each item: monospace text, muted color
- Hover: card background, text becomes `--fg`
- Mobile: 2 columns, then 1 column at 400px

### FAQ Accordion (`.faq-list`)
- Each item: button with question + `+` icon
- Answer hidden with `max-height: 0; overflow: hidden`
- Open state: `max-height: 300px`, icon rotates 45deg
- Only one open at a time (others close on toggle)

### CTA Section (`.cta-wrap`)
- Flex layout: text left, TV canvas right
- Desktop gap: 48px
- CTA button: accent background, white text, shine-on-hover effect, lift on hover
- TV Canvas: 220x220 static noise effect with overlaid image, scanlines, glitch effect
- Mobile: column-reverse, full-width button and canvas

### Footer
- Three-part flex: logo, social links, copyright
- Max-width 860px centered
- Mobile: stacked column, centered

---

## Interactive Features

### Theme Toggle
- Button in nav toggles `data-theme` attribute on `<body>`
- Text switches between "DARK" / "LIGHT"
- All color transitions are `.4s`

### Language Switcher (i18n)
- Three languages: EN, LV (Latvian), RU (Russian)
- Uses `data-i18n` attributes on elements
- Translations stored in `window.__TR` object (inline in HTML)
- Ticker items stored in `window.__TICKER` object
- Flow canvas labels are also language-aware
- Selection persists in `localStorage` as `findr-lang`

### Scroll Reveal
- Elements with `.reveal` class start invisible (`opacity: 0; translateY: 24px`)
- `IntersectionObserver` adds `.visible` class at `threshold: 0.08`
- Transition: `.6s` opacity and transform

### Canvas Animations
1. **Flow Canvas**: Continuous bezier curve animation with glowing dots
2. **TV Canvas**: Static noise + image overlay + scanlines + random glitch effect

---

## Responsive Breakpoints

| Breakpoint    | Changes                                                        |
|---------------|----------------------------------------------------------------|
| `<= 700px`   | Nav padding shrinks, social links hidden, flow canvas taller (420px), sections 32px/16px padding, steps/tasks 2-col, footer stacked, CTA reversed to column |
| `<= 400px`   | Steps and tasks become single column                           |

---

## Animation Reference

| Name       | Type       | Duration | Easing  | Description                          |
|------------|-----------|----------|---------|--------------------------------------|
| `fadeUp`   | Keyframe  | 0.8–1s   | default | Translate Y 20px + fade in           |
| `ticker`   | Keyframe  | 22s      | linear  | Infinite horizontal scroll           |
| `.reveal`  | Transition| 0.6s     | default | Scroll-triggered fade + slide up     |
| Flow dots  | rAF       | continuous| —      | Bezier path traversal with glow      |
| TV noise   | rAF       | continuous| —      | Random pixel noise + scanlines       |

---

## File Structure

```
findr-web/
  index.html    — Single-file app (HTML + CSS + JS, ~177KB)
  SKILL.md      — This file (design system documentation)
  MEMORY.md     — Project status and memory index
```

The entire site is a single self-contained HTML file. All CSS is in a `<style>` block (lines 8–100). All JS is in a `<script>` block (lines 196–329). Translations and ticker data are in inline script blocks (lines 196–197, massive JSON objects).

---

## External Links

| Destination     | URL                              | Usage                    |
|-----------------|----------------------------------|--------------------------|
| Telegram (DM)   | https://t.me/gtfindr             | CTA "send your task"     |
| X / Twitter      | https://x.com/findrdesk          | Nav + footer social      |
| Telegram (channel)| https://t.me/findrdesk         | Nav + footer social      |

---

## Development Rules

### Do NOT
- Change the accent color `#ff4500` — it is the brand identity
- Use any CSS framework (Tailwind, Bootstrap, etc.)
- Break the single-file structure unless explicitly migrating to a build system
- Add dependencies or build tools unless explicitly approved
- Remove or modify the i18n system — all user-facing text must support EN/LV/RU
- Change the font pairing (Space Mono + DM Sans)

### DO
- Use CSS custom properties for all colors
- Keep all headings, labels, buttons, and UI text in Space Mono
- Keep body/paragraph text in DM Sans
- Maintain the 860px max-width content constraint
- Ensure all new sections follow the `.section.reveal` pattern
- Add `data-i18n` attributes to any new user-facing text
- Add translations to all three languages in `window.__TR`
- Test both light and dark themes
- Test at mobile (< 700px) and narrow mobile (< 400px)
- Use the 1px-gap grid technique for new card grids
- Follow the existing naming convention: lowercase, hyphenated BEM-lite classes

### Adding a New Section
1. Add HTML: `<div class="section reveal">` with `.section-label`, `<h2>`, content
2. Add `data-i18n` keys to all text elements
3. Add translations to `window.__TR` for EN, LV, RU
4. Style with existing CSS custom properties
5. Test theme toggle and language switcher
6. Test all three responsive breakpoints
