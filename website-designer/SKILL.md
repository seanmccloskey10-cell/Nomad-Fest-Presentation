---
name: website-designer
description: Transforms a basic webpage into a premium branded product. Use when asked to design, style, or visually upgrade a website. Applies a complete visual system including typography, animated gradients, glassmorphism, marquee conveyor belt, and hover polish.
---

# Website Designer

You are a specialist web designer. When invoked, read `index.html` in the current directory and transform it into a premium product using the visual system below. Apply every component. Do not skip sections for brevity.

---

## Visual System

### Typography
- Import from Google Fonts: `Barlow Condensed:wght@700` + `Inter:wght@400;500;600`
- All headings: Barlow Condensed, uppercase, `font-weight: 700`, `letter-spacing: 0.02em`
- Body text: Inter
- Hero headline: `font-size: clamp(3.5rem, 9vw, 8rem)`, `line-height: 0.92`

```css
:root {
  --font-display: 'Barlow Condensed', sans-serif;
  --font-body:    'Inter', sans-serif;
}
body { font-family: var(--font-body); }
h1, h2, h3 {
  font-family: var(--font-display);
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.02em;
}
```

---

### Animated Gradient Hero
Apply to the hero section. Routes coral → gold → hot pink → purple → ocean blue — shared hues between each stop so there are no jarring jumps.

```css
.hero {
  background: linear-gradient(-45deg, #f4511e, #f9a825, #e91e8c, #9c27b0, #0ea5e9, #f4511e);
  background-size: 500% 500%;
  animation: gradient-shift 18s ease infinite;
}
@keyframes gradient-shift {
  0%   { background-position: 0% 50%; }
  50%  { background-position: 100% 50%; }
  100% { background-position: 0% 50%; }
}
```

**⚠️ Never anchor with a dark colour** — it kills the vivid stops and the gradient goes flat. Start and end with a vivid colour.

---

### Frosted Glass Nav
Fixed position, full width, sits above hero.

```css
nav {
  position: fixed;
  top: 0; left: 0; right: 0;
  z-index: 100;
  padding: 14px 32px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: rgba(255,255,255,0.08);
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
  border-bottom: 1px solid rgba(255,255,255,0.1);
}
```

---

### Glassmorphism Cards
Use on cards that sit over a vivid gradient background. Needs something colourful behind it to show the effect.

```css
.glass-card {
  background: rgba(255,255,255,0.12);
  backdrop-filter: blur(20px) saturate(180%);
  -webkit-backdrop-filter: blur(20px) saturate(180%);
  border: 1px solid rgba(255,255,255,0.25);
  border-radius: 16px;
  box-shadow: 0 32px 80px rgba(0,0,0,0.25), inset 0 1px 0 rgba(255,255,255,0.3);
}
```

**⚠️ Canvas + glassmorphism:** If adding a `<canvas>` element (e.g. a game), the canvas must be a **sibling** to the glass card — never inside it. `backdrop-filter` on a container that wraps a canvas freezes the canvas render loop.

---

### CSS Marquee Conveyor Belt
Two identical sets of items inside one flex container. Animates `translateX(-50%)` for a seamless loop.

```css
.marquee-bar { background: #060b14; overflow: hidden; }
.marquee-wrap { display: flex; overflow: hidden; }
.marquee-track {
  display: flex;
  flex-shrink: 0;
  animation: marquee-scroll 28s linear infinite;
}
.marquee-track:hover { animation-play-state: paused; }
@keyframes marquee-scroll {
  from { transform: translateX(0); }
  to   { transform: translateX(-50%); }
}
```

HTML structure — two identical sets (second has `aria-hidden="true"`):
```html
<div class="marquee-bar">
  <div class="marquee-wrap">
    <div class="marquee-track">
      <!-- Set 1 -->
      <div class="marquee-item">Item A</div>
      <div class="marquee-item">Item B</div>
      <!-- Set 2 — identical -->
      <div class="marquee-item" aria-hidden="true">Item A</div>
      <div class="marquee-item" aria-hidden="true">Item B</div>
    </div>
  </div>
</div>
```

---

### Hover Polish

Cards lift and glow:
```css
.card {
  transition: transform 0.2s, box-shadow 0.2s, border-color 0.2s;
}
.card:hover {
  transform: translateY(-6px);
  box-shadow: 0 16px 40px rgba(0,0,0,0.4), 0 0 20px rgba(244,81,30,0.15);
  border-color: rgba(244,81,30,0.3);
}
```

List rows slide with accent border:
```css
.list-row:hover {
  transform: translateX(5px);
  border-left: 3px solid #f4511e;
}
```

---

### Scroll Reveal
```js
function initReveal() {
  document.querySelectorAll('.reveal').forEach((el, i) => {
    el.style.opacity = '0';
    el.style.transform = 'translateY(28px)';
    el.style.transition =
      `opacity 0.55s cubic-bezier(0.25,0.46,0.45,0.94) ${i * 90}ms,
       transform 0.55s cubic-bezier(0.25,0.46,0.45,0.94) ${i * 90}ms`;
  });
  const obs = new IntersectionObserver(entries => {
    entries.forEach(e => {
      if (e.isIntersecting) {
        e.target.style.opacity = '1';
        e.target.style.transform = 'translateY(0)';
      }
    });
  }, { threshold: 0.15 });
  document.querySelectorAll('.reveal').forEach(el => obs.observe(el));
}
document.addEventListener('DOMContentLoaded', initReveal);
```

Add `.reveal` to each game card, each player row, the stats section, membership section. Do NOT unobserve — elements stay visible when the presenter scrolls back up.

---

## Restraint Rules

Apply without exception:

- **One gradient treatment only** — the hero. Not on buttons, not on text elsewhere
- **Frosted glass buttons** when on the hero: `background: rgba(255,255,255,0.18)` + `backdrop-filter: blur(10px)` + `border: 1px solid rgba(255,255,255,0.3)`
- **No floating particles** — looks like 2014 WordPress
- **No animated gradient borders on buttons** — fragile and reads as a developer trick
- **No more than one animated element** per section

---

## Emoji + Gradient Text

Never put an emoji inside a gradient text span — it renders as a coloured blob.

```html
<!-- ✅ correct -->
<h1>🏓 <span class="gradient-text">SMASH CLUB</span></h1>

<!-- ❌ wrong -->
<h1 class="gradient-text">🏓 SMASH CLUB</h1>
```

---

## Output

Apply the full visual system to `index.html`. Preserve all existing content and functionality — only add design. Return a single complete `index.html` file.
