# Workshop Structure — 20-Minute Time Breakdown

---

## Overview

| Segment | Time | Duration | What Happens |
|---------|------|----------|--------------|
| Hook | 0:00 | 1:30 | The "raise your hand" moment |
| Setup | 1:30 | 0:30 | Context: what we're building and why |
| Build #1 | 2:00 | 4:30 | Pickleball site from zero — single prompt |
| Reaction | 6:30 | 1:00 | Show the result, let it land |
| Bridge | 7:30 | 1:30 | What most people get wrong, intro Plan Mode |
| Build #2 | 9:00 | 6:30 | Plan Mode → reaction game |
| Reaction | 15:30 | 1:00 | Demo the game live, audience reaction |
| Pitch | 16:30 | 2:00 | Code Explorer, WHOP, Preply |
| Q&A / Close | 18:30 | 1:30 | Questions + QR code on screen |

---

## Detailed Breakdown

---

### 0:00 — Hook (1 min 30 sec)

**Goal:** Get hands in the air. Make them feel the gap between ideas and execution.

**Say:**
> "Quick show of hands — who here has an idea for an app, a website, a tool... something you'd build if you could? Keep your hand up."
>
> *[pause — most hands go up]*
>
> "Now keep it up if you don't know how to code."
>
> *[most stay up — usually gets a laugh]*
>
> "Perfect. This is for you. I'm going to show you how to go from that idea... to a working website... in under two minutes. No code. No designers. No developers. Just you and an AI."

**Why this works:** Starts with participation. Validates non-coders before a single line of code appears.

---

### 1:30 — Setup (30 sec)

**Goal:** Frame the build. Pickleball is the right choice — everyone knows it, no domain knowledge needed.

**Say:**
> "We're building a pickleball website. Why pickleball? Because you're going to see exactly what's possible in two minutes — and pickleball is something everyone gets. No jargon, no niche. Just a community sports site, built live in front of you."

*[Claude Code already open in VS Code, full screen, font large enough for back row]*

---

### 2:00 — Build #1: The Speed Demo (4 min 30 sec)

**Goal:** Paste the prompt. Watch Claude build. Say almost nothing while it runs — let the build speak.

**What to do:**
1. Paste Prompt 1 from `lesson/PROMPTS.md`
2. Hit enter
3. Step back slightly from the keyboard
4. Narrate loosely while it builds (script in `02-LIVE-BUILD-SCRIPT.md`)
5. When it finishes, open the browser / preview

**Time buffer:** Prompt 1 should complete in 60–90 seconds. You have 4.5 minutes total for this segment, so there's room for a slow connection or a second run if something minor breaks.

**If it's building fast and looks done early:**
Don't rush to the next segment. Let the audience absorb it. Ask "What do you see?" Give them 30 seconds to look.

---

### 6:30 — Reaction Moment (1 min)

**Goal:** Let the wow land. Don't undersell it.

**Say:**
> "There it is. From nothing. A working website — games section, leaderboard, a sign-up form. Functional."
>
> *[pause 3-4 seconds — let the plainness register]*
>
> "Now — notice it's basic. No branding, no identity, no personality. That's on purpose. Because the next prompt is where it becomes something real."

**Don't:** Rush into Phase 2. The contrast is the point — give them a moment to absorb how plain it looks before the transformation.

---

### 7:30 — Bridge to Plan Mode (1 min 30 sec)

**Goal:** Set up the need for Plan Mode. Make them feel the problem before you show the solution.

**Say:**
> "Now here's where most people get stuck. They see that, they get excited, they start prompting randomly. 'Make it prettier.' 'Add a game.' 'Give it a brand.' And Claude does its best — but without a plan, you get chaos. Features that clash. Code that breaks. A site that falls apart."
>
> "The fix is something called Plan Mode. Before Claude writes a single line, it thinks through the whole problem. What needs to happen? In what order? What could go wrong? It's the difference between a contractor who just swings a hammer... and one who reads the blueprints first."
>
> "I'm going to ask Claude to invent a brand identity, redesign this entire site around it, and add a working game — all in one prompt. But first, it plans. Watch what happens."

---

### 9:00 — Build #2: Plan Mode (6 min 30 sec)

**Goal:** Enable Plan Mode. Paste Prompt 2. Let the audience see Claude think before it builds. Then approve and watch it build.

**What to do:**
1. Enable Plan Mode (shift+tab in Claude Code, or verbal explanation if using claude.ai)
2. Paste Prompt 2 from `lesson/PROMPTS.md`
3. While Plan Mode runs, narrate what's happening (script in `02-LIVE-BUILD-SCRIPT.md`)
4. Show the plan before approving — point out 2-3 specific items
5. Approve and let it build
6. Open the browser, play the game live

**Time buffer:** Plan Mode + build could take 3-4 minutes total. You have 6.5 minutes. Use the extra time to narrate, zoom in on the plan output, or play the game multiple times.

---

### 15:30 — Play the Game (1 min)

**Goal:** Make it tangible and fun. Play it live on screen. If the crowd is interactive, invite someone up.

**Say:**
> "Look at this. Same site — completely different product. Claude invented the name, picked the colors, built the hero, redesigned every section. And added a working game."
>
> *[scroll to the game section, click Play, react visibly to the ball]*
>
> "287 milliseconds. The game works. And this" — *[scroll back to top]* — "is a real branded product. From a plain HTML page. In about six minutes."

---

### 16:30 — Course Pitch (2 min)

**Goal:** Light, confident, specific. Not a sales pitch — more like "here's what I do if you want to go further."

**Say:**
> "What you just saw — that's what I teach. I run a course called Code Explorer. It's on a platform called WHOP, which most of you probably know."
>
> "It's for people exactly like the ones with their hands up at the start. You have ideas. You don't code. I take you from that point to shipping real apps — not toy demos, real things you can share, sell, or use."
>
> "I also teach one-on-one on Preply if you want to go faster with someone alongside you. $40 an hour, and most students ship their first real project in the first session."
>
> "QR code is on screen. Scan it, save it, come find me after. Happy to answer questions."

*[QR code slide — links to WHOP course or linktree]*

---

### 18:30 — Q&A / Close (1 min 30 sec)

**Say:**
> "Two minutes for questions — what's on your mind?"

**Common questions to prep for:**
- "Do I need to pay for Claude?" → Yes, ~$20/month. Worth it immediately.
- "Can I really build something real with this?" → Yes — but you need to learn the prompting patterns. That's what the course teaches.
- "What's the difference between this and ChatGPT?" → Claude Code builds actual files and runs locally. It's purpose-built for making things.
- "How do you deploy it?" → One command — netlify deploy. I show that in the course too.

---

## Timing Risk Areas

| Risk | Mitigation |
|------|-----------|
| Build #1 takes too long | Pre-warm Claude, have backup recording |
| Plan Mode is slow or verbose | Pre-explain: "this is normal, it's thinking" |
| Game doesn't work first try | "Let me just tweak one thing" — have fix ready |
| Questions eat into demo time | Park complex questions: "grab me after" |
| Crowd is quiet / flat | Ask directly: "what do you notice?" — forces engagement |
