# 5ED Web Design System
## Reference Guide for All Web Pages & Landing Pages

---

## Overview

This document defines the visual language for all 5ED web properties (landing pages, marketing pages, dashboards, web views). It serves as the source of truth so any new page matches the established look and feel.

**Aesthetic:** Dark, athletic, premium. Feels like a sports brand crossed with a fintech app — not a school project, not a generic fitness app. Clean enough to feel professional, bold enough to feel exciting for teens.

**Direction:** RTL Hebrew-first. All layouts, text alignment, and interactions flow right-to-left.

---

## Colors

### Core Palette

| Token | Hex | Usage |
|-------|-----|-------|
| `--orange` | `#FF8714` | Brand primary. CTAs, accents, highlights, active states. The signature Five Fingers color. |
| `--orange-glow` | `#FF871440` | Subtle radial glows behind hero sections, hover shadows. 25% opacity of orange. |
| `--dark` | `#0A0A0F` | Page background. Near-black with a slight blue undertone — never pure `#000`. |
| `--dark-card` | `#141419` | Card/surface background. One step lighter than page bg. |
| `--dark-border` | `#1E1E26` | Borders, dividers, subtle separators. Low contrast, never harsh. |
| `--white` | `#FFFFFF` | Primary text, headings. |
| `--light-gray` | `#C5C5CF` | Body text, descriptions. Readable on dark bg without being stark white. |
| `--gray` | `#8E8E9A` | Secondary text, labels, hints, timestamps. |
| `--green` | `#22C55E` | Success states, active indicators, positive metrics. |

### Rules

- **Background is always dark.** No light theme. The app lives in dark mode.
- **Orange is for action and emphasis only.** If everything is orange, nothing is. Use it for: CTA buttons, key numbers/stats, highlighted words in headings, active/selected states, the brand mark.
- **Text hierarchy uses white → light-gray → gray.** Headings are white. Body is light-gray. Secondary info is gray.
- **Never use pure black `#000000` for backgrounds.** Always `#0A0A0F` or similar with slight color warmth.
- **Colored backgrounds are rare.** If used, they're subtle gradients or radial glows, not solid blocks.

### CSS Variables

```css
:root {
  --orange: #FF8714;
  --orange-glow: #FF871440;
  --dark: #0A0A0F;
  --dark-card: #141419;
  --dark-border: #1E1E26;
  --white: #FFFFFF;
  --gray: #8E8E9A;
  --light-gray: #C5C5CF;
  --green: #22C55E;
}
```

---

## Typography

### Font Stack

| Role | Font | Weight(s) | Usage |
|------|------|-----------|-------|
| Display / Headings | **Oswald** | 600, 700 | All headings (h1–h3), stat numbers, CTAs, navigation, labels, section titles |
| Body / UI | **Heebo** | 400, 500, 700, 900 | Body text, form labels, descriptions, buttons (secondary), UI elements |

**Why these fonts:**
- **Oswald** is angular, condensed, and athletic. It reads as strong and purposeful — perfect for a youth fitness brand. It also renders well in Hebrew.
- **Heebo** is a clean Hebrew-first font designed for screen readability. It pairs naturally with Oswald — one is loud, the other is quiet.

### Loading

```html
<link href="https://fonts.googleapis.com/css2?family=Heebo:wght@400;500;700;900&family=Oswald:wght@600;700&display=swap" rel="stylesheet">
```

### Scale

| Element | Font | Size | Weight | Color | Notes |
|---------|------|------|--------|-------|-------|
| Hero heading (h1) | Oswald | `clamp(40px, 10vw, 72px)` | 700 | white | Line-height 1.05, letter-spacing -0.02em |
| Section heading (h2) | Oswald | `clamp(28px, 6vw, 40px)` | 700 | white | Highlighted word in `<em>` uses orange |
| Card heading (h3) | Oswald | 18px | 700 | white | — |
| Section label | Oswald | 13px | 600 | orange | Uppercase, letter-spacing 0.12em |
| Body text | Heebo | 16px | 400 | light-gray | Line-height 1.8 |
| Small text / descriptions | Heebo | 14px | 400 | gray | Line-height 1.6 |
| Tiny text / notes | Heebo | 12-13px | 400 | gray | Form notes, footer |
| Stat number | Oswald | 36px | 700 | orange | — |
| CTA button text | Oswald | 20px | 700 | dark (on orange bg) | — |

### Heading Patterns

```html
<!-- Section label + heading combo (most common) -->
<div class="section-label">LABEL TEXT</div>
<h2>First line of heading<br><em>Highlighted part</em></h2>

<!-- The <em> inside headings is always orange, never italic -->
h2 em { color: var(--orange); font-style: normal; }
```

---

## Spacing & Layout

### Max Width

- **Content sections:** `max-width: 640px` centered
- **Full-width sections:** Edge to edge, content still 640px max
- **Form sections:** `max-width: 480px` centered

### Padding

| Context | Padding |
|---------|---------|
| Section (desktop) | `80px 24px` (top/bottom, left/right) |
| Section (mobile) | `60px 20px` |
| Card internal | `24px` |
| Form section | `80px 24px 100px` |

### Gap Patterns

| Between | Gap |
|---------|-----|
| Cards in a list | `24px` |
| Form fields | `16px` |
| Grid columns (form row) | `16px` |
| Stats in a row | `40px` (desktop), `24px` (mobile) |

### Border Radius

| Element | Radius |
|---------|--------|
| Cards | `16px` |
| Buttons (CTA) | `14px` |
| Input fields | `12px` |
| Badges / pills | `100px` |
| Small elements (avatars, icons) | `10-12px` |

---

## Components

### Cards

```css
.card {
  background: var(--dark-card);
  border: 1px solid var(--dark-border);
  border-radius: 16px;
  padding: 24px;
}
```

- Always have a `1px solid var(--dark-border)` border — this creates subtle depth without shadows
- Hover state: `border-color: var(--orange)` with slight transform
- No drop shadows — the grain texture and borders handle depth

### Buttons

**Primary CTA (orange):**
```css
.cta-btn {
  background: var(--orange);
  color: var(--dark);
  font-family: var(--font-display); /* Oswald */
  font-size: 20px;
  font-weight: 700;
  padding: 16px 40px;
  border-radius: 14px;
  border: none;
  transition: all 0.3s cubic-bezier(.4,0,.2,1);
}

.cta-btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 12px 40px var(--orange-glow);
}
```

- Text is always `var(--dark)` on orange background (high contrast)
- Hover lifts up 2px and adds an orange glow shadow
- Disabled state: `opacity: 0.5`, no transform, no shadow

**No secondary button style defined yet.** If needed: ghost style with `border: 1px solid var(--orange)`, `color: var(--orange)`, transparent background.

### Form Inputs

```css
input, select, textarea {
  background: var(--dark-card);
  border: 1px solid var(--dark-border);
  border-radius: 12px;
  padding: 14px 16px;
  font-family: var(--font-body);
  font-size: 16px;
  color: var(--white);
}

input:focus, select:focus, textarea:focus {
  border-color: var(--orange);
}
```

- Focus state = orange border. No outline, no glow.
- Labels above inputs: 14px, weight 500, light-gray
- Placeholder text: inherits gray from browser default
- Phone/number inputs: `dir="ltr"` even in RTL layout
- Select dropdown arrow: custom SVG, positioned left (because RTL)

### Badges / Pills

```css
.badge {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  background: var(--dark-card);
  border: 1px solid var(--dark-border);
  padding: 8px 16px;
  border-radius: 100px;
  font-size: 13px;
  color: var(--orange);
  font-weight: 500;
}
```

- Used for status indicators, tags, labels
- Optional green dot (`::before` pseudo-element) for "active" state with pulse animation

### Step / List Items

```css
.step {
  display: flex;
  gap: 20px;
  align-items: flex-start;
  background: var(--dark-card);
  border: 1px solid var(--dark-border);
  border-radius: 16px;
  padding: 24px;
}
```

- Number or emoji on the right (RTL), content on the left
- Step number: Oswald, 32px, bold, orange
- Title: Oswald, 18px, bold, white
- Description: Heebo, 14px, gray

### Coach Bubble

```css
.coach-bubble {
  background: #1E1E26;
  border-radius: 14px 14px 4px 14px; /* RTL: sharp corner bottom-right */
  padding: 14px 18px;
  font-size: 14px;
  line-height: 1.7;
  color: var(--light-gray);
}
```

- Coach avatar: 36px square, orange background, rounded 10px, emoji inside
- Bubble has asymmetric border-radius (one sharp corner = speech direction)
- `<strong>` inside bubbles is white (default bold behavior)

---

## Effects & Atmosphere

### Grain Texture

A fixed SVG noise overlay at 3% opacity covers the entire page. This adds subtle texture to the dark backgrounds, preventing the "flat screen" feel.

```css
body::before {
  content: '';
  position: fixed;
  inset: 0;
  background-image: url("data:image/svg+xml,..."); /* SVG feTurbulence noise */
  pointer-events: none;
  z-index: 9999;
  opacity: 0.03;
}
```

**Always include this.** It's a signature element of the 5ED web aesthetic.

### Orange Glow

Radial gradient glow used behind hero sections and special cards:

```css
.element::before {
  content: '';
  position: absolute;
  width: 600px;
  height: 600px;
  background: radial-gradient(circle, var(--orange-glow) 0%, transparent 70%);
  pointer-events: none;
}
```

- Used sparingly — hero section and one or two highlight areas max
- Always `position: absolute` with the parent as `position: relative; overflow: hidden`
- Never so strong that it washes out text readability

### No Shadows

We don't use `box-shadow` for depth. Depth comes from:
1. Background color steps (`--dark` → `--dark-card` → `#1E1E26`)
2. Border lines (`--dark-border`)
3. The grain texture
4. Orange glow for emphasis

Exception: CTA hover state uses `box-shadow: 0 12px 40px var(--orange-glow)` — this is a glow, not a depth shadow.

---

## Animation

### Philosophy

- **Entrance animations only.** Elements animate in once when they enter the viewport. No looping animations except subtle indicators (pulse dot, scroll hint).
- **Fast and purposeful.** 0.5-0.8s duration. Cubic-bezier easing. Nothing bouncy or playful — this is athletic and sharp.
- **Staggered reveals.** When multiple cards enter, they animate with slight delays (80ms between each) for a cascading effect.

### Scroll Reveal

```css
.reveal {
  opacity: 0;
  transform: translateY(30px);
  transition: all 0.6s cubic-bezier(.4,0,.2,1);
}

.reveal.visible {
  opacity: 1;
  transform: translateY(0);
}
```

Triggered by IntersectionObserver at `threshold: 0.15`:

```javascript
const observer = new IntersectionObserver((entries) => {
  entries.forEach((entry, i) => {
    if (entry.isIntersecting) {
      setTimeout(() => entry.target.classList.add('visible'), i * 80);
      observer.unobserve(entry.target);
    }
  });
}, { threshold: 0.15 });
```

### Hero Entrance

Hero elements use CSS `animation` with staggered `animation-delay`:

```css
@keyframes fadeUp {
  from { opacity: 0; transform: translateY(24px); }
  to { opacity: 1; transform: translateY(0); }
}

/* Stagger: badge 0s, h1 0.1s, subtitle 0.2s, CTA 0.3s, stats 0.4s */
.badge { animation: fadeUp 0.8s ease both; }
h1 { animation: fadeUp 0.8s ease 0.1s both; }
```

### Hover States

- **Cards:** `border-color: var(--orange)` + slight translate (`translateX(-4px)` in RTL)
- **Buttons:** `translateY(-2px)` + orange glow shadow
- **Transition:** `all 0.3s cubic-bezier(.4,0,.2,1)` — never `ease` or `linear`

### Micro-animations

- **Pulse dot:** Green indicator dot with `opacity` keyframe (2s loop)
- **Scroll hint:** Gentle vertical bounce (2s loop, 1.5s delay so it starts after hero loads)

---

## Responsive Behavior

### Breakpoints

Only one breakpoint needed for most pages:

```css
@media (max-width: 480px) {
  /* Mobile adjustments */
}
```

### Mobile Rules

- Stats row: reduce gap from 40px to 24px, numbers from 36px to 28px
- Form rows: stack to single column (`grid-template-columns: 1fr`)
- Section padding: reduce from `80px 24px` to `60px 20px`
- Coach bubbles: `max-width` from 85% to 92%
- Hero heading uses `clamp()` so it scales automatically

### Mobile-First Principles

- Touch targets: minimum 44px height for all interactive elements
- `font-size: 16px` minimum on inputs (prevents iOS zoom)
- `maximum-scale=1.0` in viewport meta (prevents pinch zoom on forms)
- `100svh` for hero height (respects mobile browser chrome)

---

## RTL Specifics

### Global

```html
<html lang="he" dir="rtl">
```

### Patterns

- Text alignment flows naturally from `dir="rtl"`
- Flex layouts: `gap` works correctly; no need for `flex-direction: row-reverse`
- Form labels are right-aligned by default
- Phone number inputs: add `dir="ltr"` explicitly
- Select dropdown arrow: positioned on the **left** side (opposite of LTR)
- Card hover translate: use `translateX(-4px)` (moves left in RTL = away from reading edge)
- Coach bubble border-radius: sharp corner is bottom-right (`14px 14px 4px 14px`)

---

## Page Structure Template

```html
<!DOCTYPE html>
<html lang="he" dir="rtl">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0">
  <title>5ED — [Page Title] | חמש אצבעות</title>
  
  <!-- OG tags for WhatsApp/social sharing -->
  <meta property="og:title" content="...">
  <meta property="og:description" content="...">
  
  <!-- Fonts -->
  <link href="https://fonts.googleapis.com/css2?family=Heebo:wght@400;500;700;900&family=Oswald:wght@600;700&display=swap" rel="stylesheet">
  
  <style>
    :root { /* all CSS variables */ }
    /* Grain overlay on body::before */
    /* Sections, components, animations */
  </style>
</head>
<body>

  <!-- HERO: always full-viewport, centered, with orange glow -->
  <!-- CONTENT SECTIONS: max-width 640px, 80px vertical padding -->
  <!-- CTA / FORM SECTION: max-width 480px -->
  <!-- FOOTER: simple, centered, border-top -->

  <script>
    // IntersectionObserver for reveals
    // Smooth scroll for anchor links
  </script>
</body>
</html>
```

---

## Brand Mark

The 5ED logo appears as text, not an image:

```html
<div class="footer-logo">5<span>ED</span> × חמש אצבעות</div>
```

- "5" in white, "ED" in orange
- Font: Oswald, 20px, bold
- The "×" separates the product name from the organization name
- No logo image file exists yet — text mark is the current identity

---

## Do's and Don'ts

### Do

- Use the grain texture overlay on every page
- Keep headings in Oswald, body in Heebo — never mix
- Use orange sparingly: CTAs, stats, emphasis words
- Animate elements on scroll entry (once, not looping)
- Test on mobile first — most users come from WhatsApp
- Use `clamp()` for responsive font sizes
- Keep cards consistent: dark-card bg + dark-border border + 16px radius

### Don't

- Use light/white backgrounds — ever
- Use box-shadow for depth (use border + color steps)
- Use more than one accent color (orange is it)
- Make everything orange — it loses impact
- Use looping animations beyond status indicators
- Use Inter, Roboto, Arial, or system fonts
- Use generic purple-on-white AI aesthetics
- Put Hebrew body text in Oswald — it's for headings only