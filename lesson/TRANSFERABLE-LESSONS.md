# Transferable Lessons — From the Nomad Fest Presentation

**What this is:** Lessons from building and red-teaming the Nomad Fest 20-minute presentation (SMASH CLUB pickleball site). Written for the Claude agent working on the Nomad Workshop (Nomad Finder, 45 minutes, 4 prompts).

**How to use this:** Read it once at session start alongside the existing workshop docs. It doesn't replace them — it adds guard rails that were discovered the hard way.

---

## The Single Most Important Lesson: The Reference File

The biggest live demo risk is Claude writing complex code from scratch under time pressure and producing bugs — broken canvas physics, a marquee that doesn't loop, a glob that won't render. The fix is a **reference file**.

**How it works:**
- Before the demo, save pre-tested, working implementations of every complex component into a reference file (e.g. `lesson/IMPLEMENTATION-GUIDE.md` or a dedicated `lesson/CODE-REFERENCE.md`)
- Add one line to the relevant prompt: *"Before writing any code, read `lesson/CODE-REFERENCE.md` and use those implementations for [component X]."*
- Claude reads pre-tested code and integrates it rather than writing from scratch

**For the Nomad Workshop specifically — the highest-risk components are:**

| Component | Risk | Why |
|-----------|------|-----|
| Globe.gl initialisation | Very high | Needs exact sequence: init → texture → dots → autoRotate AFTER init |
| Globe autoRotate on city select | High | Easy to forget `globe.controls().autoRotate = false` — globe spins away from selected city |
| Netlify function + API call | Very high | API key path, function file structure, netlify.toml redirect — multiple failure points |
| Wizard modal | Medium | Progress bar, 4 steps, back/next state management |

If any of these components are already working from a dry run, save the exact working code into the implementation guide so Claude can reproduce it reliably.

---

## Per-Prompt Backup Snapshots

Save a working copy of the HTML after each prompt completes successfully. Before the demo, have all four snapshots ready.

```
backup/
  prompt1-result.html   ← plain foundation
  prompt2-result.html   ← design + globe working
  prompt3-result.html   ← interactivity working
  prompt4-result.html   ← AI wizard working (full final)
```

**Why four levels:** If something breaks during Prompt 3, you don't have to abandon the demo — open `prompt2-result.html` and continue narrating from there. The audience doesn't know it was pre-built.

**The fallback hierarchy:**
1. One follow-up fix prompt: *"Read the implementation guide and fix [specific thing]."*
2. Open the snapshot from the last working prompt
3. If all else fails, open the final `prompt4-result.html` and demo that

Never retry the same broken approach three times. One fix attempt, then open the snapshot.

---

## "Premium = Restraint" — Visual Decision Rule

This was the key red-team finding from the presentation. Applies equally to the workshop.

**The test for every visual effect:** Does this look like a designer made a deliberate choice, or does it look like a developer found a trick?

**Cut without hesitation:**
- Floating particles — looks like 2014 WordPress or a crypto page
- Animated gradient borders on buttons (`@property` CSS) — fragile, reads as developer trick
- Too many gradient elements — one gradient headline = design choice, three = visual chaos

**Keep:**
- One strong gradient treatment (header/title)
- Glassmorphism on a card that has something vivid behind it (works because Globe.gl background can be set transparent, letting the page colour show through)
- Hover lift + glow on cards — subtle, everyone notices
- Typography upgrade — non-technical audiences register "professional" primarily through fonts

---

## The Contrast IS the Lesson

Prompt 1 is intentionally plain. This is not a failure — it's the setup for the wow moment.

**For the Nomad Workshop:**
- Prompt 1 should be obviously basic — title, subtitle, dark background, system font
- Resist the urge to add anything nice to Prompt 1
- The more basic it looks, the more dramatic the Prompt 2 transformation feels

If Prompt 1 looks polished, Prompt 2 looks like iteration. If Prompt 1 looks rough, Prompt 2 looks like magic.

---

## Demo Moves — Know What to Point At

After each prompt finishes, have specific things ready to demonstrate. Don't just scroll — interact.

**After Prompt 2 (Design + Globe):**
- Point at the gradient title — "Claude picked the font and colour scheme"
- Watch the globe auto-rotate — let it spin for 3 seconds before touching anything
- Globe dots glowing cyan — point at them: "that's the city data"

**After Prompt 3 (Interactivity):**
- Click a city in the list — globe zooms there and stops
- Click a different city — globe smoothly transitions
- Open an accordion — the data expands inline

**After Prompt 4 (AI Wizard):**
- Click "✨ Find My Perfect City" — show the modal opening
- Go through all 4 steps — let the audience call out their choices
- Watch the globe fly to the AI's recommendation — this is the climax

**The AI recommendation moment is your version of "pong game in one prompt."** Build to it.

---

## Known Technical Gotchas (from the Nomad Workshop docs + additional)

These are already documented in `lesson/IMPLEMENTATION-GUIDE.md` but worth having in one place:

- Globe.gl needs explicit `width` and `height` on its container — without it, the globe won't render
- Separate the 🌍 emoji from the gradient `<span>` — emoji inside gradient CSS renders as a coloured blob
- `autoRotate` must be set AFTER globe initialisation, not before
- `globe.controls().autoRotate = false` on city select — otherwise globe spins away from selected city
- Netlify reads `.env.local` over `.env` if both exist
- Kill all node processes before `netlify dev` — port 3999 conflicts are silent failures
- Prompt 4 API call: use regular JSON response, not streaming — streaming is unreliable in live demos
- The "Find My Perfect City" button should be visible from Prompt 2 but non-functional — don't wire it up early

---

## Time Budget (45 minutes)

| Segment | Target time |
|---------|-------------|
| Intro + context | 3 min |
| Prompt 1 (type + build) | 3 min |
| Show Prompt 1, react | 1 min |
| Prompt 2 (type + build + globe loads) | 6 min |
| Demo Prompt 2 moves | 2 min |
| Prompt 3 (type + build) | 7 min |
| Demo Prompt 3 moves | 3 min |
| Prompt 4 (type + build + AI call test) | 10 min |
| Live AI demo with audience input | 5 min |
| Q&A / takeaways | 5 min |

**If you're running behind:** Prompt 3 interactivity is the most skippable — you can jump to Prompt 4 with hardcoded city data pre-filled and the audience won't notice. Prompt 4's AI moment is the payoff — protect it.

---

## Slash Commands Worth Adding

The presentation uses `/prep` to delete the working file and display both prompts before the demo. For the workshop, consider:

- `/prep` — kill node processes, confirm backup snapshots exist, display all 4 prompts
- `/snapshot` — save current `index.html` to `backup/promptX-result.html` at the right moment

---

*Source: Nomad Fest Presentation project — lessons from multiple dry runs and red-team sessions.*
*Last updated: 2026-03-17*
