# Implementation Guide — Nomad Fest Demo

This is the source of truth. Every dry run must produce the same output.
If the result looks different from what's described here, something is wrong — fix it before the next run.

---

## Prompt 1 — Plain Foundation

### Goal
A real business website that looks competent but not designed. Audience thinks "that's impressive for one prompt." Then Prompt 2 hits and they think "wait, what just happened."

The contrast is the lesson. Do not make Prompt 1 too polished.

### Exact layout (top to bottom)
1. **Nav** — plain sticky bar. Logo "The Pickleball Court" + 3 text links (Book a Court / Leaderboard / Membership). No CTA button, no frosted glass.
2. **Hero** — dark navy background. Headline "Book a Court. Play Today." Short tagline (2 lines max). Two plain buttons.
3. **Stats bar** — 4 stats in a row: 6 Courts / 320+ Members / 4.9★ Google / Open 7 Days. Plain numbers on dark background.
4. **Upcoming Games** — 3 cards. Date, time, location, skill level as plain text. No colored badges.
5. **Leaderboard** — simple table. Rank / Player / Wins / Win Rate. No flags, no streaks column.
6. **Membership** — two-column: perks list (plain checkmarks) + sign-up form (name, email, skill level dropdown, submit button).
7. **Footer** — venue address, Da Nang Vietnam.

### Style rules for Prompt 1
- `background: #050e18` (dark navy) — the ONLY background color
- **Two colors only: navy + white.** No orange, no green, no accent colors anywhere
- System fonts only — no Google Fonts
- White text at varying opacity for hierarchy (headings 100%, body 65%, labels 45%)
- CTA buttons: white background + navy text (primary), white border (secondary)
- No hover effects, no transitions, no animations
- No colored skill badges — just plain muted text labels
- No emoji flags in the leaderboard
- "Competent template" — not "premium product." The wow is speed, not design.

### What Prompt 1 must NOT have
- Google Fonts
- Gradient backgrounds
- Glassmorphism
- Pong game
- Marquee conveyor belt
- Scroll-reveal animations
- Hover effects on cards

---

## Prompt 2 — Full Brand Transformation

### How the demo works
`rm -f index.html` before each run. Claude builds from scratch:
- **Prompt 1** → plain dark navy site (~2 min build)
- **Prompt 2** → `/website-designer` skill + brand name + pong game (~3 min build)

The `/website-designer` skill reads `website-designer/SKILL.md` which instructs Claude to:
1. Read `lesson/PROMPT2-CODE-REFERENCE.md` for pong game + marquee (pre-tested, ~250 lines — never write from scratch)
2. Apply the full visual system to `index.html`

### Exact Prompt 2 output specs (lock these down — replicate exactly)

**Brand name:** Claude invents it. Must feel like a premium sports community. Previous dry run: **RALLY CO.**

**Layout — hero section:**
- Hero is full-width, stacked vertically: hero content (headline, tagline, CTAs) at top, game card centered below
- NOT side-by-side columns — stacked with `flex-direction: column; align-items: center`
- Game card: `max-width: 540px`, centered

**Gradient hero:**
```css
background: linear-gradient(-45deg, #f4511e, #f9a825, #e91e8c, #9c27b0, #0ea5e9, #f4511e);
background-size: 500% 500%;
animation: gradient-shift 35s ease infinite;  /* 35s — slow and smooth, not jarring */
```

**Pong game — exact speed values:**
```js
const BASE_SPEED = 7;    // slow enough to be playable, fast enough to look alive
const aiSpeed = 5;       // AI paddle speed
```

**Headline treatment:**
```css
background: linear-gradient(135deg, #ffffff 0%, #f9a825 55%, #f4511e 100%);
-webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text;
```
One gradient text treatment only. Not on buttons.

**Hero tagline:** Short, punchy. Two lines max. E.g.: "6 courts. 320+ members. Open every day. Da Nang's home of pickleball."

**Section backgrounds (alternating — gives the page depth):**
| Section | Background |
|---------|-----------|
| Hero | Animated CSS gradient |
| Stats | `#1e293b` dark slate (marquee belt) |
| Games | `#050e18` navy |
| Leaderboard | `#0a1628` navy-mid |
| Membership | `linear-gradient(135deg, #0a1628, #0f0a28, #0a1628)` dark purple |
| Footer | `#020912` near-black |

**Typography:**
- Barlow Condensed 700 — all headings, uppercase
- Inter 400/500/600 — body
- Hero h1: `clamp(3.5rem, 8vw, 7rem)`, `line-height: 0.92`

**Glassmorphism card:**
```css
background: rgba(255,255,255,0.18);
backdrop-filter: blur(20px) saturate(180%);
border: 1px solid rgba(255,255,255,0.35);
box-shadow: 0 32px 80px rgba(0,0,0,0.25), inset 0 1px 0 rgba(255,255,255,0.4);
```

**Frosted glass nav:**
```css
background: rgba(255,255,255,0.08);
backdrop-filter: blur(20px);
border-bottom: 1px solid rgba(255,255,255,0.1);
```

**Hover polish:**
- Game cards: `translateY(-6px)` + coral glow shadow on hover
- Leaderboard rows: `translateX(4px)` + coral left border on hover

**Scroll-reveal:** `.reveal` on game cards, leaderboard rows, membership section. 90ms stagger. Do not unobserve.

**Marquee stats belt:** Uses pre-tested HTML+CSS from `lesson/PROMPT2-CODE-REFERENCE.md`. Stats: 6 Courts / 320+ Members / Open 7 Days a Week / 4.9★ / 🌴 Da Nang, Vietnam / Book A Court Today.

### Do NOT build
- Multiple HTML files
- Floating particles
- Animated gradient borders on buttons
- Light/dark mode
- Mobile layout

---

## Live Demo Moves (after Prompt 2 finishes)

1. Point at the typography — "Claude picked the font"
2. Watch the hero gradient cycling — slow and smooth at 35s
3. Click ▶ Play on the pong game — move mouse over court to play
4. Hover a game card — lifts and glows
5. Scroll down slowly — cards reveal with stagger
6. Scroll to marquee — stats belt scrolling continuously

---

## Guard Rails

### Speed strategy
The `/website-designer` skill now automatically reads `lesson/PROMPT2-CODE-REFERENCE.md` first. This means Claude integrates pre-tested pong game (~250 lines) and marquee code rather than writing them from scratch. Build time: ~2-3 min instead of ~5-8 min.

### Time budget (20 minutes)
| Time | Action |
|------|--------|
| 0:00 | Intro + context |
| 2:00 | Prompt 1 — type and submit |
| 4:30 | Prompt 1 result — open browser, react with audience |
| 5:30 | Prompt 2 — type and submit (`/website-designer` + brand + pong) |
| 8:30 | Prompt 2 result — open browser, do live demo moves |
| 11:30 | Explain the skill concept |
| 13:30 | Q&A / takeaways |

### Fallbacks
**Level 1:** If Prompt 2 output is broken, follow up: "Fix the [game / marquee / gradient] — check `lesson/PROMPT2-CODE-REFERENCE.md`." One attempt only.

**Level 2:** Open `backup/smash-club-branded.html` silently. Audience doesn't know it was pre-built.

**Emergency git recovery:** `git checkout solution -- index.html`
