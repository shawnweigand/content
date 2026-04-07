# DESIGN.md — AI Roadmap Guide
> Visual language, component library, and layout system for the AI Roadmap HTML guide.

---

## 1. Design Philosophy

This guide is built around **clarity with depth** — a document someone can skim from 10,000 feet or drill into without losing their place. The aesthetic leans **editorial-technical**: precise typography, calm dark surfaces, and purposeful accent color used only when something truly matters.

**Core principles:**
- Every visual element earns its place by reducing cognitive load
- Phases and milestones are legible at a glance, explorable on demand
- Motion is subtle — it orients, never distracts
- Content hierarchy is structural, not decorative

---

## 2. Color System

### Base Palette

| Token                 | Light Mode    | Dark Mode     | Usage                          |
|-----------------------|---------------|---------------|--------------------------------|
| `--color-bg`          | `#F7F6F2`     | `#0F1017`     | Page background                |
| `--color-surface`     | `#FFFFFF`     | `#181B24`     | Card / panel surfaces          |
| `--color-surface-2`   | `#F0EEE9`     | `#1E2130`     | Subtle inset sections          |
| `--color-border`      | `#E3E0D8`     | `#2A2F40`     | Dividers, card borders         |
| `--color-text-primary`| `#1A1A1A`     | `#E8E6E0`     | Headings, primary body         |
| `--color-text-muted`  | `#6B6860`     | `#7A7D8A`     | Metadata, subtitles, captions  |

### Accent Ramp — Indigo

Used sparingly: active states, progress indicators, CTAs, highlighted milestones.

| Stop   | Hex       | Usage                              |
|--------|-----------|-------------------------------------|
| `50`   | `#EEF0FD` | Hover fills, badge backgrounds      |
| `200`  | `#B0B8F5` | Subtle borders on active elements   |
| `500`  | `#5B67E8` | Primary accent, links, indicators   |
| `700`  | `#3A45C0` | Hover/pressed accent states         |
| `900`  | `#1E2475` | Text on light accent fills          |

### Status Colors

| State       | Hex       | Token Suggestion           |
|-------------|-----------|----------------------------|
| Complete    | `#1D9E75` | `--color-success`          |
| In Progress | `#BA7517` | `--color-warning`          |
| Not Started | `#888780` | `--color-neutral`          |
| Blocked     | `#D85A30` | `--color-danger`           |

---

## 3. Typography

### Typeface Stack

```css
/* Display / Headings */
font-family: 'DM Serif Display', 'Georgia', serif;

/* Body / UI */
font-family: 'IBM Plex Sans', 'system-ui', sans-serif;

/* Code / Metadata */
font-family: 'IBM Plex Mono', 'Courier New', monospace;
```

### Scale

| Role             | Size     | Weight  | Line Height | Usage                          |
|------------------|----------|---------|-------------|--------------------------------|
| Display          | `3rem`   | `400`   | `1.1`       | Hero title                     |
| H1               | `2rem`   | `400`   | `1.2`       | Section titles                 |
| H2               | `1.375rem`| `500`  | `1.3`       | Phase headers                  |
| H3               | `1.125rem`| `500`  | `1.4`       | Milestone titles               |
| Body             | `1rem`   | `400`   | `1.7`       | Descriptions, explanations     |
| Small / Meta     | `0.8125rem`| `400` | `1.5`       | Tags, dates, captions          |
| Mono / Code      | `0.875rem`| `400`  | `1.6`       | Inline code, skill labels      |

**Rules:**
- Sentence case everywhere. No ALL CAPS except design tokens.
- Heading color: `--color-text-primary`. Never use accent color for heading text.
- Max line length: `72ch` for body text. Cards may be narrower.
- Never set `font-weight` above `600`.

---

## 4. Spacing & Layout

### Base Unit
`8px`. All spacing is a multiple of this unit.

### Spacing Scale

| Token      | Value  | Use                                |
|------------|--------|------------------------------------|
| `--sp-1`   | `4px`  | Icon-to-label gap, tight pairs     |
| `--sp-2`   | `8px`  | List item padding, badge padding   |
| `--sp-3`   | `12px` | Inline component padding           |
| `--sp-4`   | `16px` | Card internal padding (small)      |
| `--sp-5`   | `24px` | Card padding, section gaps         |
| `--sp-6`   | `32px` | Section breathing room             |
| `--sp-8`   | `48px` | Major section separators           |
| `--sp-10`  | `64px` | Page section top padding           |

### Grid
- Max content width: `1100px`, centered
- Column system: CSS Grid, `repeat(12, 1fr)`, `gap: 24px`
- Phase cards: span 12 on mobile, span 6 on tablet, span 4 on desktop
- Sidebar (if used): `280px` fixed, main content fluid

### Border Radius

| Token        | Value  | Used for                       |
|--------------|--------|--------------------------------|
| `--r-sm`     | `4px`  | Tags, badges, inline pills     |
| `--r-md`     | `8px`  | Buttons, inputs                |
| `--r-lg`     | `12px` | Cards, panels                  |
| `--r-xl`     | `20px` | Hero sections, large surfaces  |

---

## 5. Component Library

### 5.1 Phase Card
The primary container for each roadmap phase.

```
┌──────────────────────────────────┐
│  Phase 1 · Q1 2025              │  ← Phase label (small, muted)
│  Foundation                     │  ← Phase title (H2, serif)
│  ─────────────────────────────  │
│  Short description of this       │  ← Body text
│  phase's goals and outcomes.     │
│                                  │
│  [●] Milestone A     Complete    │  ← Milestone rows
│  [◐] Milestone B     In Progress │
│  [○] Milestone C     Planned     │
│                                  │
│  [View Details →]                │  ← CTA (optional)
└──────────────────────────────────┘
```

**Specs:**
- Background: `--color-surface`
- Border: `0.5px solid var(--color-border)`
- Border radius: `--r-lg` (`12px`)
- Padding: `--sp-5` (`24px`)
- Box shadow: none by default; `0 0 0 2px var(--color-accent-200)` on hover/focus

### 5.2 Milestone Row

```html
<div class="milestone">
  <span class="milestone__status milestone__status--complete"></span>
  <span class="milestone__label">Deploy RAG pipeline</span>
  <span class="milestone__badge milestone__badge--complete">Complete</span>
</div>
```

**Status indicator sizes:** `10px` circle, `border-radius: 50%`  
**Badge:** `font-size: 0.75rem`, `padding: 2px 8px`, `border-radius: --r-sm`

### 5.3 Progress Bar

Used at the top of phase cards to show phase-level completion.

```
[████████░░░░░░] 54%
```

**Specs:**
- Track: `height: 4px`, `border-radius: 2px`, `background: --color-border`
- Fill: `background: --color-accent-500` (with status-based variants)
- Label: `font-size: 0.75rem`, positioned right-aligned above or beside bar

### 5.4 Tag / Skill Badge

Inline label for tagging skills, tools, or domains to a milestone.

```
[Python]  [LangChain]  [Vector DB]
```

**Specs:**
- Font: `--font-mono`, `0.75rem`
- Background: `--color-surface-2`
- Border: `0.5px solid --color-border`
- Padding: `2px 8px`
- Border radius: `--r-sm`
- Color: `--color-text-muted`

### 5.5 Timeline Connector

Vertical line connecting phase cards in a vertical layout.

```
│
│  (dot)
│
```

- Line: `1px solid --color-border`, centered horizontally in gutter
- Node dot: `12px` circle, `2px` border, accent-colored when active
- Inactive: border `--color-border`, fill `--color-surface`
- Active / current: fill `--color-accent-500`

### 5.6 Section Header

Used to open major roadmap sections (e.g., "Phases Overview", "Skills Map").

```
Skills Map                         ← H1, serif
──────────────────────────────────  ← 1px divider, --color-border
Tools and capabilities to build    ← Body, muted
across each phase of the journey.
```

### 5.7 Hero / Page Header

```
AI Roadmap                                 ← Display, serif
Your path from zero to production AI.     ← Body subtitle
─────────────────────────────────────────
[ Phase 1 ] [ Phase 2 ] [ Phase 3 ]       ← Jump nav (optional)
```

---

## 6. Motion & Animation

All animation must be purposeful and subtle. Zero decorative animation.

| Event               | Property         | Duration  | Easing                     |
|---------------------|------------------|-----------|----------------------------|
| Card hover          | `box-shadow`     | `150ms`   | `ease-out`                 |
| Phase expand/collapse | `max-height`, `opacity` | `250ms` | `ease-in-out`      |
| Progress bar fill   | `width`          | `600ms`   | `cubic-bezier(0.22,1,0.36,1)` |
| Page load stagger   | `opacity`, `translateY` | `400ms` + `delay` | `ease-out`   |
| Status badge update | `opacity`        | `200ms`   | `ease`                     |

**Rules:**
- All animations behind `@media (prefers-reduced-motion: no-preference)`
- No infinite loops except loading spinners (which are hidden once content loads)
- Stagger page-load reveals with `animation-delay: calc(var(--i) * 60ms)`

---

## 7. Iconography

- Icon set: **Lucide** (consistent stroke weight `1.5`)
- Size: `16px` for inline icons, `20px` for standalone action icons, `24px` for section markers
- Color: inherits `currentColor` — never hardcoded
- Never use icons as the sole differentiator; always pair with a text label

Status icons:
| Status       | Icon name          |
|--------------|--------------------|
| Complete     | `check-circle`     |
| In Progress  | `circle-dot`       |
| Not Started  | `circle`           |
| Blocked      | `circle-x`         |

---

## 8. Accessibility

- Minimum contrast ratio: `4.5:1` for body text, `3:1` for large text and UI components
- All interactive elements: visible `:focus-visible` ring — `0 0 0 2px --color-accent-500`, `offset: 2px`
- Cards and expandable sections: keyboard-navigable (`tabindex`, `aria-expanded`)
- Status badges: include `aria-label` with full status text, never rely on color alone
- Avoid `display: none` for expandable content — use `visibility: hidden` + `height: 0` or `aria-hidden`
- Skip-to-content link at top of page

---

## 9. Dark Mode

Dark mode is mandatory. All colors defined via CSS custom properties and switched with:

```css
@media (prefers-color-scheme: dark) {
  :root {
    --color-bg: #0F1017;
    --color-surface: #181B24;
    /* etc. */
  }
}
```

Or toggled manually via `data-theme="dark"` on `:root` for a user toggle.

**Rules:**
- Never hardcode hex values in component CSS — always reference tokens
- Test every component in both modes before shipping
- Surface elevation in dark mode is achieved through slight lightening of `--color-surface-2`, not shadows

---

## 10. File & Asset Conventions

```
/
├── index.html
├── DESIGN.md          ← this file
├── styles/
│   ├── tokens.css     ← all CSS custom properties
│   ├── base.css       ← reset, typography, global rules
│   ├── components.css ← reusable component styles
│   └── layout.css     ← grid, page structure
├── scripts/
│   └── roadmap.js     ← interactivity, accordion, progress
└── assets/
    └── icons/         ← SVG icons if self-hosted
```

**CSS naming convention:** BEM — `.block__element--modifier`  
**Breakpoints:**

| Name    | Min width |
|---------|-----------|
| `sm`    | `480px`   |
| `md`    | `768px`   |
| `lg`    | `1024px`  |
| `xl`    | `1280px`  |

---

*Last updated: April 2025 · AutoMates / AI Roadmap Guide*