# DESIGN.md — Claude Visual Identity & Design System

---

## Overview

This guide defines the visual language for all Claude-related presentations, slides, and UI components. Every visual should feel like it belongs to the same system — dark, precise, intelligent, and quietly confident. Not flashy. Not corporate. Not generic AI.

The aesthetic direction is: **refined dark-mode editorial**. Think technical documentation meets luxury product design. High contrast. Intentional spacing. Typography that earns attention.

---

## Color Palette

### Primary Background
```
--color-bg-base:        #0A0A0A   /* Near-black. Default page/slide background. */
--color-bg-surface:     #111111   /* Cards, panels, elevated surfaces. */
--color-bg-elevated:    #1A1A1A   /* Modals, dropdowns, tooltips. */
--color-bg-border:      #222222   /* Subtle dividers and borders. */
```

### Claude Brand Accent
```
--color-accent-primary: #CC785C   /* Warm terracotta/coral. Claude's signature tone. */
--color-accent-soft:    #E8956D   /* Lighter variant for hover states and highlights. */
--color-accent-muted:   #7A3F2A   /* Darker variant for pressed states or deep accents. */
```

### Text
```
--color-text-primary:   #F0EDE8   /* Warm off-white. Primary headings and body copy. */
--color-text-secondary: #A09A92   /* Muted warm gray. Subheadings, captions, labels. */
--color-text-tertiary:  #5A554F   /* Very muted. Placeholders, disabled states. */
--color-text-inverse:   #0A0A0A   /* For text on light accent backgrounds. */
```

### Semantic / Layer Colors
Each architecture layer has a dedicated accent used in diagrams, pyramid segments, and callouts:
```
--color-layer-model:    #CC785C   /* Model — terracotta (primary accent) */
--color-layer-context:  #7B9E87   /* Context — sage green */
--color-layer-tools:    #6B8CAE   /* Tools — steel blue */
--color-layer-skills:   #9B7BB8   /* Skills — dusty violet */
--color-layer-agents:   #C4A44A   /* Agents — warm gold */
```

### Utility
```
--color-success:        #5A8A6A   /* Muted green. Confirmations, passing evals. */
--color-warning:        #C4A44A   /* Warm gold. Caution states. */
--color-error:          #A04040   /* Muted red. Errors, failures. */
--color-code-bg:        #141414   /* Terminal and code block backgrounds. */
--color-code-text:      #A8C090   /* Monospace text — muted green on dark. */
```

---

## Typography

### Typeface Pairing
| Role | Font | Weight | Usage |
|---|---|---|---|
| Display | **Fraunces** | 300–700 | Hero titles, section headers, pyramid labels |
| Body | **DM Sans** | 300–500 | Body copy, descriptions, captions |
| Mono | **DM Mono** | 400 | Code blocks, terminal output, commands, file names |

All three are available via Google Fonts.

### Type Scale
```
--text-hero:    clamp(3rem, 6vw, 5.5rem)   /* Presentation hero title */
--text-h1:      clamp(2rem, 4vw, 3.5rem)   /* Section title */
--text-h2:      clamp(1.4rem, 2.5vw, 2rem) /* Part title / slide subheading */
--text-h3:      1.25rem                    /* Card title */
--text-body:    1rem                       /* Body copy */
--text-small:   0.875rem                   /* Captions, labels, tags */
--text-mono:    0.85rem                    /* Code, terminal, commands */
```

### Type Rules
- **Headings**: Fraunces, sentence case, light tracking (`letter-spacing: -0.02em` for large sizes)
- **Body**: DM Sans, 1.6 line-height, warm off-white or secondary text color
- **Commands and file names**: DM Mono, always wrapped in a `--color-code-bg` pill or block
- **Never use**: Inter, Roboto, Arial, system-ui as display fonts
- **Avoid**: All-caps on large headings. Use it sparingly on labels and tags only.

---

## Spacing & Layout

### Base Unit
All spacing is derived from an 8px base unit.
```
--space-1:   4px
--space-2:   8px
--space-3:   12px
--space-4:   16px
--space-6:   24px
--space-8:   32px
--space-12:  48px
--space-16:  64px
--space-24:  96px
```

### Layout Principles
- **Generous padding**: Slide content should never crowd edges. Minimum 48–64px inset on all sides.
- **Controlled density**: Cards and components breathe. Don't pack elements.
- **Asymmetry when intentional**: Diagrams and hero layouts can break grid for impact.
- **Consistent gutters**: 24px between cards, 48px between major sections.

---

## Surface & Depth

### Cards & Panels
```css
background:    var(--color-bg-surface);
border:        1px solid var(--color-bg-border);
border-radius: 12px;
padding:       32px;
```

For elevated/featured cards, add a subtle glow:
```css
box-shadow: 0 0 0 1px rgba(204, 120, 92, 0.15),
            0 8px 32px rgba(0, 0, 0, 0.4);
```

### Dividers
Use `--color-bg-border` (`#222222`) for all horizontal rules and borders. Never use pure white dividers on dark backgrounds.

### Layer Accent Bars
When a component is associated with a specific pyramid layer, add a 3px left border or top bar using that layer's color variable.

---

## Iconography & Diagrams

### Style
- **Line icons only**: Stroke weight 1.5–2px. Rounded caps. No filled icons unless used as glyphs.
- **Icon color**: `--color-text-secondary` by default. Use accent color only on active or highlighted states.
- **Icon size**: 20px standard, 24px in cards, 16px in labels.

### Diagram Rules
- All diagrams use `--color-bg-base` or `--color-bg-surface` as background
- Connector lines: 1px, `--color-bg-border` default, accent color when active
- Node labels: DM Sans small, `--color-text-secondary`
- Highlighted nodes: `--color-accent-primary` border + soft glow
- Arrow heads: minimal, filled triangle, same color as connector line

### Pyramid Diagrams
- Rendered as a stacked series of trapezoid shapes
- Each tier uses its dedicated `--color-layer-*` variable as a left border or fill with low opacity (10–15%)
- Active/highlighted tier gets full opacity fill and a brighter border
- Layer name in Fraunces, descriptor in DM Sans small below

---

## Motion & Animation

### Principles
- **Purposeful only**: Animate to communicate, not to decorate
- **Fast and precise**: 150–300ms for UI transitions. 400–600ms for reveals
- **Easing**: `cubic-bezier(0.16, 1, 0.3, 1)` for entrances. `ease-in` for exits.

### Standard Transitions
```css
/* Default UI transition */
transition: all 200ms cubic-bezier(0.16, 1, 0.3, 1);

/* Entrance reveal */
@keyframes fadeUp {
  from { opacity: 0; transform: translateY(12px); }
  to   { opacity: 1; transform: translateY(0); }
}
animation: fadeUp 400ms cubic-bezier(0.16, 1, 0.3, 1) forwards;

/* Staggered list reveal */
animation-delay: calc(var(--index) * 80ms);
```

### Hover States
- Cards: `transform: translateY(-2px)` + slightly brighter border
- Buttons: background shifts to `--color-accent-soft`
- Links: color shifts to `--color-text-primary`, underline animates in

---

## Buttons & Interactive Elements

### Primary Button
```css
background:    var(--color-accent-primary);
color:         var(--color-text-inverse);
font-family:   'DM Sans', sans-serif;
font-size:     0.875rem;
font-weight:   500;
padding:       10px 20px;
border-radius: 8px;
border:        none;
```

### Secondary Button
```css
background:    transparent;
color:         var(--color-text-primary);
border:        1px solid var(--color-bg-border);
```

### Ghost / Label Tags
```css
background:    rgba(204, 120, 92, 0.1);
color:         var(--color-accent-primary);
border:        1px solid rgba(204, 120, 92, 0.25);
border-radius: 4px;
padding:       2px 8px;
font-family:   'DM Mono', monospace;
font-size:     0.75rem;
```

---

## Code & Terminal Blocks

```css
background:    var(--color-code-bg);
color:         var(--color-code-text);
font-family:   'DM Mono', monospace;
font-size:     0.85rem;
line-height:   1.7;
border-radius: 8px;
padding:       20px 24px;
border:        1px solid var(--color-bg-border);
```

Terminal windows should include a three-dot header row (red/yellow/green dots at 8px diameter) in `--color-bg-elevated` to establish the terminal frame.

---

## Tone & Visual Personality

- **Dark by default**: Never use a white or light background unless explicitly inverted for contrast effect
- **Warm neutrals over cold grays**: The palette leans warm — off-white, terracotta, sage — never pure blue-gray
- **Confident whitespace**: Empty space is intentional, not accidental
- **No gradients as backgrounds**: Use solid surfaces. Gradients are reserved for glows, accents, and layer fills at low opacity
- **No drop shadows for decoration**: Shadows communicate elevation only
- **Restraint on accent color**: `--color-accent-primary` should feel special. Use it on one element per visual unit.

---

## Do / Don't

| ✅ Do | ❌ Don't |
|---|---|
| Dark backgrounds with warm off-white text | White or light gray backgrounds |
| Fraunces for display headings | Inter, Roboto, or system fonts |
| DM Mono for all commands and file paths | Backtick-only code inline in body text |
| Layer colors from the defined palette | Random accent colors |
| Subtle borders to define surfaces | Heavy drop shadows for decoration |
| Generous padding inside cards | Cramped or edge-touching content |
| Animate reveals on scroll or load | Continuous looping animations |
| Sentence case on headings | ALL CAPS HEADINGS |

---

*This document is the source of truth for all Claude presentation and UI visuals. When in doubt, default to restraint, warmth, and precision.*