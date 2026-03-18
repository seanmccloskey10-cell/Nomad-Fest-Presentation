# Nomad Fest — Live Build Prompts

Two prompts. Prompt 1 is plain on purpose — the contrast makes Prompt 2 hit harder.

---

## PROMPT 1 — Foundation

> Build a pickleball membership website for a venue in Da Nang, Vietnam.
>
> Include a nav, a hero section with headline and CTA, a stats bar, upcoming games with skill levels, a top players leaderboard, a membership signup section, and a footer.
>
> Dark navy background, system fonts. Real marketing copy — make it feel like an actual business. No design or styling beyond the basics.

---

## PROMPT 2 — Make It a Product

> /website-designer
>
> Invent a premium brand name for this pickleball club. Add a live pong game in the hero glass card — use the implementation in `lesson/PROMPT2-CODE-REFERENCE.md`.

That's it. `/website-designer` handles the full visual transformation. The brand name and pong game are the only additions.

---

## Key Elements Checklist

### Prompt 1 — must hit these
- [ ] Dark navy background (`#050e18`)
- [ ] Nav + hero + stats bar + games + leaderboard + membership form + footer
- [ ] Real marketing copy (not placeholder Lorem Ipsum)
- [ ] System fonts only — no Google Fonts yet

### Prompt 2 — must hit these
- [ ] Start with `/website-designer`
- [ ] Invent a brand name
- [ ] Pong game in hero (from reference file)

---

## Why This Works

**Prompt 1 is a real business site, not a toy.** The audience needs to be impressed by Prompt 1 — and then floored by Prompt 2. "That's already good" → "wait, what just happened."

**`/website-designer` is a skill, not a magic word.** It's a set of design instructions Claude reads and applies. The audience learns: AI can hold reusable expertise, not just answer questions.

**Pong in the hero is the crowd moment.** After Prompt 2 finishes, click Play. A fully playable game, embedded on a webpage, from one sentence. Let the silence do the work.

**Claude invents the brand.** More impressive than you choosing the name. Audience watches an identity appear from nothing.

---

## What to Avoid

- **Plan Mode** — this demo shows skill, not planning
- **Floating particles** — looks like 2014 WordPress
- **Animated gradient borders on buttons** — reads as developer trick
- **Multiple HTML files** — single `index.html` only
- **Writing pong from scratch** — always use `lesson/PROMPT2-CODE-REFERENCE.md`
