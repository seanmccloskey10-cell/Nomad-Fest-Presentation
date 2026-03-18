# SMASH CLUB — Nomad Fest Presentation

This is a **20-minute live coding demo** for 200+ non-technical entrepreneurs at Nomad Fest. The goal is to show what's possible with AI-assisted development in two prompts.

**What gets built:** A pickleball membership website for a Da Nang, Vietnam venue. Prompt 1 is intentionally plain. Prompt 2 transforms it into a premium branded product.

---

## The Two-Prompt Demo

### Prompt 1 — Build a real business website (plain, no design)

The output must look like a real business, not a student project. Dark navy background, proper marketing copy, full layout. See exact spec in `lesson/IMPLEMENTATION-GUIDE.md` → Prompt 1 section.

**Required sections (top to bottom):**
1. Fixed nav — logo + 3 nav links
2. Hero — strong headline, Da Nang tagline, CTA button
3. Stats bar — 6 courts, 320+ members, 4.9★ rating, open 7 days
4. Upcoming games — 3 sessions with date, location, skill badge
5. Top players leaderboard — rank, name, wins
6. Membership section — perks + signup form
7. Footer — venue address, Da Nang Vietnam

**Style:** Dark navy `#050e18`, system fonts only, solid layout, real marketing copy. No custom typography, no gradients, no animations. "Polished template" — not "premium product." The contrast with Prompt 2 is the whole lesson.

### Prompt 2 — `/website-designer` + brand + pong game

Uses the `/website-designer` skill to apply the full visual system. The skill reads `website-designer/SKILL.md`. Additionally:
- Invent a brand name (premium sports community feeling)
- Add a live pong game in the hero glass card — use implementation from `lesson/PROMPT2-CODE-REFERENCE.md`
- Single HTML file

---

## Guard Rails

**Reference file:** `lesson/PROMPT2-CODE-REFERENCE.md` contains pre-tested implementations of the pong game (~250 lines) and CSS marquee. Always use these — do not write from scratch. Saves 3-5 minutes.

**Backup file:** `backup/smash-club-branded.html` is the complete finished site. Open this silently if Prompt 2 fails or runs over time.

**Solution branch:** `git checkout solution -- index.html` recovers the finished site at any point.

---

## What NOT to do

- No Plan Mode — this demo shows **skill**, not planning
- No floating particles
- No animated gradient borders on buttons
- No multiple HTML files
- Do not write the pong game from scratch — use the reference file

---

## Files

| File | Purpose |
|------|---------|
| `lesson/IMPLEMENTATION-GUIDE.md` | Full build spec for both prompts |
| `lesson/PROMPTS.md` | The exact prompts used on stage |
| `lesson/PROMPT2-CODE-REFERENCE.md` | Pre-tested pong game, marquee, gradient code |
| `website-designer/SKILL.md` | Visual design skill — applied via `/website-designer` |
| `backup/smash-club-branded.html` | Emergency fallback — complete finished site |
| `docs/` | Workshop structure, timing, backup plans |
