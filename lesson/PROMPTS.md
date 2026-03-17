# Nomad Fest — Live Build Prompts

**What we're building:** One pickleball website, built in two phases.
Phase 1 is intentionally plain — so Phase 2 hits harder.

---

## PROMPT 1 — Foundation (keep it basic)

> Build a simple pickleball website
>
> Include:
> - A header with a title and short tagline
> - An upcoming games section with 3 games (date, location, skill level)
> - A top players leaderboard with 5 players
> - A join us section with a name and email form
>
> Keep it basic for now — just structure and content, no fancy design

---

## PROMPT 2 — Brand It and Build It Out (Plan Mode first)

**Before typing this prompt: enable Plan Mode**
- Claude Code: shift+tab to toggle Plan Mode (UI turns blue)
- claude.ai: start your message with "Think carefully and make a plan before building"

> Before writing any code, read `lesson/PROMPT2-CODE-REFERENCE.md` — use those implementations for the animated gradient, pong game, and marquee.
>
> Now make this a real product.
>
> Create a brand identity from scratch — invent a name, pick a visual theme, choose a colour palette that feels like a premium sports community. Something people would actually pay to join.
>
> Then transform the full site around that brand:
> - Import Barlow Condensed and Inter from Google Fonts — use Barlow Condensed for all headings, Inter for body text
> - Style the brand name as a proper wordmark in the nav
> - Replace the hero background with the animated gradient from the reference file (coral → gold → pink → purple → blue, cycling)
> - Apply gradient text to the main headline (one treatment — not on buttons)
> - Apply glassmorphism to the game card (backdrop-filter: blur + saturate) — white glass appearance over the vivid gradient
> - Add the pong game from the reference file inside the hero glass card
> - Replace the stats bar with the CSS marquee conveyor belt from the reference file
> - Add .reveal class to cards, player rows, and sections — call initReveal() on DOMContentLoaded
> - Add data-target attributes to stat numbers — call initCountUp() on DOMContentLoaded
> - Polish hover states: card lift + glow, leaderboard row accent
> - Give each section a distinct background so the page has depth
>
> Single HTML file. Make it look like a design agency spent a week on it.

---

## Using Whispr Flow (Voice Input)

These prompts are dictated via Whispr Flow — they won't match word for word. That's fine.

**What matters is that each prompt covers the key elements below. The exact wording doesn't matter.**

### Prompt 1 — Key Elements to Hit

- [ ] Pickleball website
- [ ] Keep it basic / just structure / no design yet
- [ ] Upcoming games section (3 games)
- [ ] Leaderboard (5 players)
- [ ] Join / sign up form

### Prompt 2 — Key Elements to Hit

- [ ] Tell Claude to read `lesson/PROMPT2-CODE-REFERENCE.md` first
- [ ] Invent a brand name and visual identity (premium sports community)
- [ ] Barlow Condensed + Inter from Google Fonts
- [ ] Wordmark treatment in the nav
- [ ] Animated gradient hero (coral → gold → pink → purple → blue, cycling)
- [ ] Gradient text on main headline (not on buttons)
- [ ] Glassmorphism on game card — white glass over vivid gradient
- [ ] Pong game inside the hero glass card
- [ ] CSS marquee conveyor belt replacing the stats bar
- [ ] `.reveal` on cards/sections + call `initReveal()`
- [ ] Hover polish: card lift + glow
- [ ] Section depth: distinct background per section
- [ ] Single HTML file

---

## Why This Structure Works

**Prompt 1 is intentionally plain.**
System fonts, basic structure, no visual personality. The plainer it looks, the more dramatic the transformation in Prompt 2. Don't be tempted to add design to Prompt 1 — the contrast is the lesson.

**Prompt 2 lets Claude choose the brand.**
More impressive than picking the name yourself. The audience watches Claude invent a product in real time.

**The scaffold is honest and smart.**
Three JS functions and two CSS keyframes are pre-loaded in index.html — dormant, doing nothing. Prompt 2 applies the classes and calls the functions. Claude writes the actual transformation. This is like a contractor who already has the tools laid out — the skill is still in applying them.

**The reference file is the speed secret.**
`lesson/PROMPT2-CODE-REFERENCE.md` holds pre-tested implementations of the pong game (~250 lines) and CSS marquee. Telling Claude to read it first drops build time from ~5-8 min to ~2-3 min and eliminates the two most bug-prone components.

**Typography is the highest ROI single change.**
Non-technical audiences register "professional" primarily through fonts. Barlow Condensed for headings transforms the visual tone immediately.

**The pong game is the live demo move.**
After Prompt 2 finishes, click Play on the game inside the hero. A fully playable pong game, embedded on a webpage, built with one prompt. Audience reaction is immediate.

**Plan Mode earns its place.**
Full brand identity + typography + 6 visual effects + all section redesigns is genuinely complex. The plan output visibly reasons through multiple layers. Audience sees Claude thinking, not just producing.

---

## What to Avoid

- **Floating particles** — tested and red-teamed. Look like 2014 WordPress or crypto pages. Cut.
- **Animated gradient border on buttons** — @property CSS, fragile in live demos, reads as "developer trick" not "design choice". Cut.
- **Multiple HTML files** — always single index.html
- **Light/dark mode** — audience is desktop-only, skip
- **Mobile layout** — 200 people on a projected screen, skip
