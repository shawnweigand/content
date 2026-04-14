# DESIGN.md — AI Roadmap Presentation

> A refined, editorial design system for a clean, modern AI roadmap presentation.
> Aesthetic direction: **Quiet Precision** — the visual language of high-end strategy decks. Dark, focused, and confident. Every element earns its place.

---

## 1. Aesthetic Direction

**Theme:** Dark editorial minimalism with warm off-white type and restrained terracotta/amber accents. Inspired by luxury annual reports and high-concept product strategy decks. Not cold tech — thoughtful, human, grounded.

**Mood words:** Intentional. Measured. Strategic. Unhurried.

**What makes it memorable:** The negative space. Content breathes. Sections feel like chapters. The accent color appears rarely — and when it does, it means something.

---

## 2. Color System

| Token               | Value       | Usage                                              |
|---------------------|-------------|----------------------------------------------------|
| `--color-bg`        | `#0E0D0C`   | Primary background — near-black with warm undertone |
| `--color-surface`   | `#161513`   | Card / section backgrounds                         |
| `--color-surface-2` | `#1E1C1A`   | Elevated surfaces, hover states                    |
| `--color-border`    | `#2A2724`   | Subtle dividers, card borders                      |
| `--color-text`      | `#F0EBE3`   | Primary text — warm off-white, never pure white    |
| `--color-text-muted`| `#7A7068`   | Captions, labels, secondary info                   |
| `--color-text-dim`  | `#4A4540`   | Placeholder text, decorative elements              |
| `--color-accent`    | `#C8744A`   | Terracotta — milestone markers, highlights, CTAs   |
| `--color-accent-dim`| `#3D2418`   | Accent background tints, tag fills                 |
| `--color-line`      | `#C8744A33` | Subtle accent-tinted rule lines                    |

**Rules:**
- `--color-accent` is used sparingly — maximum 2–3 instances per slide/section.
- No pure `#FFFFFF` or `#000000` anywhere.
- No gradients except a single, barely-visible radial on the hero background.

---

## 3. Typography

### Font Stack

| Role           | Font              | Source                | Fallback          |
|----------------|-------------------|-----------------------|-------------------|
| Display        | **Canela**        | Fonts in Use / Adobe  | Georgia, serif    |
| Heading        | **Söhne**         | Klim Type Foundry     | 'DM Sans', sans-serif |
| Body           | **DM Sans**       | Google Fonts          | system-ui         |
| Mono / Labels  | **DM Mono**       | Google Fonts          | monospace         |

> If Canela or Söhne are unavailable, substitute **Fraunces** (Google Fonts) for display and **DM Sans** for headings.

### Type Scale

| Name       | Size      | Weight | Line Height | Tracking | Usage                          |
|------------|-----------|--------|-------------|----------|--------------------------------|
| `display`  | 64–80px   | 300    | 1.1         | −0.03em  | Section cover titles           |
| `h1`       | 40–48px   | 400    | 1.2         | −0.02em  | Slide headlines                |
| `h2`       | 28–32px   | 500    | 1.3         | −0.01em  | Phase / section titles         |
| `h3`       | 20–22px   | 500    | 1.4         | 0        | Card headings                  |
| `body`     | 16px      | 400    | 1.7         | 0        | Paragraph content              |
| `small`    | 13–14px   | 400    | 1.6         | +0.01em  | Captions, footnotes            |
| `label`    | 11–12px   | 500    | 1.4         | +0.08em  | Tags, eyebrows, category labels|
| `mono`     | 13px      | 400    | 1.5         | +0.02em  | Dates, codes, metadata         |

### Typography Rules
- Display font used **only** for cover titles and major chapter openers. Never body copy.
- Labels and eyebrows are **ALL CAPS** with tight tracking.
- Avoid bold (`700+`) weights for body copy — use size contrast and color instead.
- Paragraph max-width: `62ch` to preserve readability.

---

## 4. Spacing & Layout

### Base Unit
`8px` — all spacing, padding, and gaps are multiples of 8.

### Spacing Scale

| Token      | Value  | Common Use                        |
|------------|--------|-----------------------------------|
| `--s-1`    | 4px    | Inline micro gaps                 |
| `--s-2`    | 8px    | Tight component padding           |
| `--s-3`    | 16px   | Default internal padding          |
| `--s-4`    | 24px   | Card padding                      |
| `--s-5`    | 32px   | Section sub-gaps                  |
| `--s-6`    | 48px   | Between components                |
| `--s-7`    | 64px   | Section vertical rhythm           |
| `--s-8`    | 96px   | Hero / cover breathing room       |
| `--s-9`    | 128px  | Between major chapters            |

### Grid

- **Max content width:** `1120px`, centered
- **Columns:** 12-column grid, `24px` gutters
- **Slide layout:** Full-viewport sections (`100vw × 100vh`) for presentation mode
- **Slide padding:** `80px` horizontal, `64px` vertical (desktop)
- Prefer **asymmetric layouts**: e.g., a 5-col text block paired with a 7-col visual

---

## 5. Components

### Cards
```
background:    var(--color-surface)
border:        1px solid var(--color-border)
border-radius: 4px
padding:       32px
```
- No box shadows — use border only.
- On hover: `background` shifts to `--color-surface-2`, border to `#3A3530`.
- Transition: `200ms ease` on background and border-color.

### Tags / Labels
```
font:           DM Mono, 11px, 500, uppercase, +0.08em tracking
padding:        4px 10px
border-radius:  2px
background:     var(--color-accent-dim)
color:          var(--color-accent)
```

### Rule / Divider
```
height:   1px
background: var(--color-border)
```
Use `var(--color-line)` (accent-tinted) only for milestone or chapter-break dividers.

### Timeline Node
```
width / height:  10px circle
background:      var(--color-accent)
border:          2px solid var(--color-bg)
outline:         1px solid var(--color-accent)
```
Connecting lines: `1px dashed var(--color-border)`.

### Progress / Phase Bar
```
height:          3px
background:      var(--color-border)
fill:            var(--color-accent)
border-radius:   2px
```

---

## 6. Iconography

- Use a **single icon family** throughout — recommended: [Lucide](https://lucide.dev/) or [Phosphor](https://phosphoricons.com/) (Regular weight).
- Icon size: `18px` standard, `14px` inline, `24px` featured.
- Icons inherit `--color-text-muted` by default; use `--color-accent` only when actively indicating state.
- No filled icons — outline / regular only.

---

## 7. Motion & Transitions

**Philosophy:** Motion reveals, never decorates. Every animation has a purpose.

| Element           | Animation                        | Duration  | Easing              |
|-------------------|----------------------------------|-----------|---------------------|
| Page / slide load | Staggered fade-up (children)     | 400ms     | `cubic-bezier(0.16, 1, 0.3, 1)` |
| Card hover        | Background + border color shift  | 200ms     | `ease`              |
| Milestone reveal  | Scale-in from 0.8, fade          | 300ms     | `ease-out`          |
| Section transition| Crossfade or slide-up            | 500ms     | `ease-in-out`       |
| Accent lines      | Width expand from 0              | 600ms     | `ease-out`          |

**Rules:**
- No looping animations anywhere in the deck.
- `prefers-reduced-motion`: all animations collapse to instant.
- Stagger delay between sibling items: `60ms` per item.

---

## 8. Slide Structure Templates

### Cover Slide
```
Layout:   Full bleed dark bg, content centered or left-anchored at 1/3 height
Elements: Eyebrow label (mono) → Display title (2–3 words) → Subtitle (body) → Date (mono, muted)
Accent:   Single thin horizontal rule (~120px wide) below eyebrow
```

### Section Opener
```
Layout:   Large chapter number (display, dim) + section title (h1) side by side
Elements: Number (decorative, --color-text-dim) | Title + 1-line description
Accent:   Left border accent (3px, --color-accent) on title block
```

### Content Slide
```
Layout:   Eyebrow + H2 headline at top, content area below (cards, list, or timeline)
Elements: Max 3–5 content items per slide
Accent:   Milestone or key stat highlighted in --color-accent
```

### Timeline / Roadmap Slide
```
Layout:   Horizontal or vertical timeline; phases as labeled segments
Elements: Phase label (label style) → Title (h3) → Description (small) → Status tag
Accent:   Current phase node in --color-accent; future nodes in --color-border
```

---

## 9. Do's and Don'ts

### ✅ Do
- Lead with generous whitespace — resist filling every corner
- Use the accent color as a signal, not decoration
- Keep slide content to one clear idea
- Align text to a consistent left margin
- Use `DM Mono` for all dates, percentages, and metadata
- Favor italic serif (display font) for emotional emphasis

### ❌ Don't
- Use purple, blue, or teal — this palette is warm and earthy only
- Add drop shadows or glows
- Use more than 2 font sizes on a single slide
- Bold body copy — use a muted color or smaller size instead
- Use emoji or clip art icons
- Center-align body paragraphs

---

## 10. File Conventions

| Asset Type         | Format         | Naming                         |
|--------------------|----------------|--------------------------------|
| Slide source       | HTML or Figma  | `slide-[number]-[slug].html`   |
| Exported slides    | PDF / PNG      | `ai-roadmap-deck-v[n].pdf`     |
| Fonts (if bundled) | WOFF2          | `fonts/[family]-[weight].woff2`|
| Icons              | SVG (inline)   | No separate icon file needed   |
| Design tokens      | CSS custom props | `tokens.css`                 |

---

*This document is the single source of truth for all visual decisions in the AI Roadmap presentation. Any deviation requires a documented reason.*