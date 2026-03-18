# Implementation Guide — SMASH CLUB Pickleball Site

---

## Prompt 1 — Foundation (intentionally plain)

### Build exactly this:

**File:** Single `index.html`

**Design:** Dark navy (#050e18), real marketing copy, feels like an actual court selling memberships.

**Business context:** One specific venue — "The Pickleball Court" in Da Nang, Vietnam. Copy is written as if selling memberships to expats and digital nomads.

**Layout — top to bottom:**
1. Nav — "The Pickleball Court" logo + Book a Court / Leaderboard / Membership links
2. Hero — "Book a Court. Play Today." headline, Da Nang tagline, "Become a Member" CTA
3. Stats bar — 6 courts, 320+ members, open 7 days, 4.9★ Google
4. Upcoming Games — 3 cards with colored skill badges (Beginner/Intermediate/Advanced)
5. Leaderboard — card rows, rank + name + wins
6. Membership section — two-column: perks copy + sign-up form
7. Footer — Da Nang, Vietnam address

**The right level for Prompt 1:**
Genuinely impressive for a first-timer — audience sees a real business website. But system fonts, basic layout, no brand identity, no visual personality, no game. "Polished template" not "premium product."

**What Prompt 2 adds that this doesn't have:**
- An invented brand name (not just "The Pickleball Court")
- Custom typography (Barlow Condensed + Inter from Google Fonts)
- Animated gradient hero (coral → gold → hot pink → purple → ocean blue, cycling)
- Glassmorphism white glass card over the vivid gradient
- A live pong game embedded in the hero
- CSS marquee conveyor belt for the stats bar
- Scroll-reveal animations on all sections
- Stats that count up when scrolled into view

**Why Da Nang works for the audience:**
Nomad Fest audience — expats, digital nomads. A pickleball court in Da Nang is something they can immediately picture using.

### Do NOT build yet:
- Any branding or custom typography
- The pong game
- Glassmorphism or gradient effects
- Google Fonts

---

## Prompt 2 — Full Brand Transformation

### How the demo works

The demo starts with **no index.html** — `rm -f index.html` before each run. Claude creates it from scratch:
- Prompt 1 → Claude writes the entire plain site
- Prompt 2 → `/website-designer` skill applies the full visual system; brand name + pong game are added on top

The `/website-designer` skill reads `website-designer/SKILL.md`. The pong game comes from `lesson/PROMPT2-CODE-REFERENCE.md`. No dormant scaffolding needed.

### What Claude invents (brand identity):
- A name that feels like a premium sports community
- A color palette — dark base with vivid accent(s)
- A visual identity that could believably be a paid membership product

### The 6 effects Prompt 2 applies (ranked by audience impact):

**1. Typography — Barlow Condensed + Inter**
Google Fonts import. Barlow Condensed 700 for all headings (uppercase, tight), Inter 400/500 for body. This single change makes non-technical eyes immediately register "professional."

```css
h1, h2, h3 { font-family: 'Barlow Condensed', sans-serif; font-weight: 700; text-transform: uppercase; }
body, p, li { font-family: 'Inter', sans-serif; }
h1 { font-size: clamp(3.5rem, 8vw, 7rem); line-height: 0.95; }
```

**2. Animated gradient hero background**
Apply directly to `.hero` — no extra element needed. Routes coral → gold → hot pink → purple → ocean blue, each colour sharing hues with its neighbour so there are no jarring jumps.

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

**3. Glassmorphism on game card + schedule cards**
`backdrop-filter: blur(20px) saturate(180%)` on `.game-card-hero` and `.game-sched-card`. White glass appearance (white semi-transparent background) over the vivid gradient hero.
**Critical:** canvas must remain a sibling to `.hero-content`, NOT inside the glass card — otherwise backdrop-filter freezes the canvas. Give schedule section its own radial gradient background so the glass has something to blur against.

**4. Gradient text on hero headline (one treatment only)**
```css
.hero h1 {
  background: linear-gradient(135deg, #ffffff 0%, var(--coral) 55%, var(--gold) 100%);
  -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text;
}
```
No gradient on buttons — one gradient headline max. Two gradient elements = developer trick. One = design choice.

**5. Scroll-reveal with stagger**
Add `.reveal` class to each `.game-sched-card`, each `.player` row, the stats section, membership section, footer. Call `initReveal()` on DOMContentLoaded. Stagger is 90ms per item — tuned for conference projection (invisible < 60ms, painful > 120ms).

**6. Hover polish**
The marquee handles stats — no separate count-up section needed. Focus hover polish:
```css
.game-sched-card:hover { transform: translateY(-6px); box-shadow: 0 16px 40px rgba(0,0,0,0.5), 0 0 20px rgba(255,92,43,0.15); border-color: rgba(255,92,43,0.3); }
.player:hover { border-left: 3px solid var(--coral); box-shadow: 0 0 16px rgba(255,92,43,0.12); }
```

### Section background depth (alternating, makes page feel crafted):
| Section | Background |
|---------|-----------|
| Hero | Animated CSS gradient (coral → gold → pink → purple → blue) |
| Stats | Dark marquee belt — contrasts with vivid hero above |
| Games | Distinct from stats — cards use glassmorphism if background is complex |
| Leaderboard | `#080c14` |
| Membership | Gradient CTA section |
| Footer | Near-black |

### Do NOT build:
- Multiple HTML files
- Floating particles (tested — looks cheap, like 2014 WordPress)
- Animated gradient border on button (tested — looks like a developer trick, not a design choice)
- Light/dark mode toggle
- Mobile-specific layout (200 desktop viewers)

---

## What the Audience Needs to See

**At the moment Prompt 2 finishes:**
Open the HTML file. The transformation should be immediately obvious above the fold: Barlow Condensed typography, gradient mesh background, frosted glass game card, gradient headline text.

**Live demo moves:**
1. Point at the typography — "Claude picked the font"
2. Watch the hero — the gradient cycles through coral → gold → pink → purple → blue
3. Click Play on the pong game — it's live and playable
4. Hover over a schedule card — it lifts and glows
5. Scroll down slowly — sections reveal with stagger
6. Scroll to stats marquee — numbers scroll past on the conveyor belt
7. Scroll to count-up stats section — numbers count up from zero

---

## Guard Rails — 20-Minute Demo Insurance

**The two biggest bottlenecks in a live build:**

| Component | Risk | Why |
|-----------|------|-----|
| Pong game JS | Very high | ~250 lines, canvas physics, AI paddle, screen flash — takes 2-4 min to write from scratch and is prone to bugs (ball stuck, paddle not moving) |
| CSS marquee | Medium | Seamless loop requires exactly two duplicate sets of items and precise translateX(-50%) — easy to get wrong |
| Typography | Low | Simple Google Fonts import + CSS variables |
| Glassmorphism | Low | 3-line backdrop-filter rule |

### The Reference File + Skill Strategy

**`/website-designer` skill** (`website-designer/SKILL.md`) handles the full visual system — typography, gradient, glassmorphism, marquee, hover polish, scroll-reveal. No need to specify these in the prompt.

**`lesson/PROMPT2-CODE-REFERENCE.md`** contains the pre-tested pong game (~250 lines) and marquee HTML. The skill alone won't write the game — the prompt must tell Claude to get it from the reference file.

Together these drop Prompt 2 build time from ~5-8 minutes to ~2-3 minutes.

### Time Budget (20-minute workshop)
- 0:00 — Intro + context (2 min)
- 2:00 — Prompt 1 typed + running (1 min to type, ~2 min to build)
- 5:00 — Prompt 1 result shown, react with audience (1 min)
- 6:00 — Prompt 2 typed (`/website-designer` + brand + pong game) — 1 min to type
- 7:00 — Claude builds Prompt 2 (~3 min with `/website-designer` skill + reference file)
- 10:00 — Open result, do live demo moves (3 min)
- 13:00 — Explain the skill concept to audience (2 min)
- 15:00 — Q&A / takeaways (5 min)

### Fallback Options (if something breaks)

**Level 1 — Reference file fix:** If Prompt 2 produces broken code, add to the conversation: "Read `lesson/PROMPT2-CODE-REFERENCE.md` and fix the [game / marquee / gradient]." Usually resolves in one follow-up.

**Level 2 — Emergency fallback file:** `backup/smash-club-branded.html` is the complete, pre-built branded site. If Prompt 2 takes too long or produces broken output, open this file silently in the browser — audience doesn't know it was pre-built.

**Never:** Force-retry a broken approach three times hoping it fixes itself. One follow-up fix attempt, then open the backup.
