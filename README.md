# Nomad Fest — Vibe Coding Live Demo

**Event:** Nomad Fest
**Format:** 20-minute live workshop
**Audience:** Non-technical entrepreneurs and digital nomads (200 people, projected screen)
**Goal:** Show that one good prompt can build a real product. Leave the audience feeling "I could do that."

---

## What We're Building

One pickleball membership site — **SMASH CLUB, Da Nang, Vietnam** — built live in two prompts.

**Prompt 1** builds a plain, functional site fast. That's the speed wow.
**Prompt 2** invents a full brand identity and transforms the site completely. That's the quality wow.

The contrast between Prompt 1 and Prompt 2 is the lesson.

---

## Before the Demo — Setup Steps

**1. Delete `index.html` so you start from a blank slate:**
```bash
rm -f index.html
```
The current `index.html` in this repo is the finished Prompt 2 result — it exists as a reference and emergency fallback, not as the starting point. The audience needs to watch Claude build it from nothing.

**2. Open Claude Code in VS Code:**
```bash
claude
```

**3. Open `lesson/PROMPTS.md` on a second screen or phone** — you'll read the key elements from it while dictating via Whispr Flow.

**4. Open the browser ready to preview** — you'll open `index.html` in the browser after Prompt 1 finishes.

---

## The Two Prompts

Full prompts and key elements checklist: `lesson/PROMPTS.md`

### Prompt 1 — Plain foundation (no design, no brand)
> Build a simple pickleball website for a court in Da Nang, Vietnam. Include a header, upcoming games section with 3 games, a top players leaderboard with 5 players, and a join us form. Keep it basic — just structure and content, no fancy design.

### Prompt 2 — Full brand transformation (enable Plan Mode first)
> Before writing any code, read `lesson/PROMPT2-CODE-REFERENCE.md` and use those implementations for the animated gradient, pong game, and marquee.
>
> Now make this a real product. Invent a brand identity — name, palette, premium sports community feel. Transform the full site: Barlow Condensed + Inter from Google Fonts, animated gradient hero, white glassmorphism game card, pong game inside the hero, CSS marquee stats belt, scroll-reveal on all sections, hover polish on cards and leaderboard rows. Single HTML file.

**Enable Plan Mode before Prompt 2:** `shift+tab` in Claude Code (UI turns blue)

---

## Demo Moves (after Prompt 2 finishes)

1. **Typography** — "Claude picked the font. Barlow Condensed."
2. **Hero gradient** — watch the colours cycle from coral to blue
3. **Click Play** — pong game, fully playable, built in one prompt
4. **Hover a card** — lifts and glows
5. **Scroll down** — sections snap into place with stagger

---

## Guard Rails

**The reference file is the speed secret.**
`lesson/PROMPT2-CODE-REFERENCE.md` contains pre-tested implementations of every complex component: animated gradient, pong game (~250 lines of canvas JS), marquee, glassmorphism. Telling Claude to read it first drops Prompt 2 build time from ~5–8 min to ~2–3 min.

**If Prompt 2 output is broken:** Add one follow-up — "Read `lesson/PROMPT2-CODE-REFERENCE.md` and fix the [game / marquee / gradient]."

**If that fails:** Open `backup/smash-club-branded.html` in the browser. The audience doesn't know it was pre-built.

---

## File Map

| File | Purpose |
|------|---------|
| `index.html` | Finished Prompt 2 result — reference + emergency fallback |
| `backup/smash-club-branded.html` | Identical copy of index.html — open if demo fails |
| `lesson/PROMPTS.md` | The two prompts + key elements checklists |
| `lesson/IMPLEMENTATION-GUIDE.md` | Full build spec, effects list, guard rails, time budget |
| `lesson/PROMPT2-CODE-REFERENCE.md` | Pre-tested code for game, marquee, gradient |
| `lesson/DRY-RUN-GUIDE.md` | How to practice, success metrics |
| `docs/` | Workshop structure, script, backup plan |

---

## Day-Of Checklist

- [ ] `rm -f index.html` — clean slate
- [ ] Claude Code open in VS Code, font bumped up for projection
- [ ] `lesson/PROMPTS.md` open on phone or second screen
- [ ] Browser open, ready to preview `index.html`
- [ ] `backup/smash-club-branded.html` ready in a background tab
- [ ] Whispr Flow running for voice input
- [ ] Wi-Fi tested — or hotspot ready as fallback
