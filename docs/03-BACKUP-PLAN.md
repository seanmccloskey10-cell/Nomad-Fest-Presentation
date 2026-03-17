# Backup Plan — When the Demo Fails

**Rule:** Always have three layers of backup. The demo failing in front of a crowd is fine — if you handle it smoothly, it's actually a teaching moment.

---

## The Three Layers

### Layer 1 — Minor Fix (demo still runs)
Something broke but Claude can fix it. You stay live.

**Triggers:** Wrong output, missing section, game doesn't function properly

**Response:**
> "This is the workflow — when something's off, you describe it back to Claude."

Then type a quick fix prompt like:
> "The game doesn't show the ball. Fix the ball spawn logic."

Claude fixes it in 30–60 seconds. Continues live.

**Why this is fine:** It shows the real iteration loop. Non-technical audience sees "oh, you just describe the problem." More instructive than a perfect first run.

---

### Layer 2 — Wi-Fi Dies / Claude Times Out
Demo can't continue. You switch to the recording.

**Before the event:** Record a full run of both builds. Save as `backup/demo-recording.mp4`

**Response:**
> "Okay — festival Wi-Fi. This is exactly why you have a backup."

*[Switch to screen recording — play it fullscreen]*

> "This is a recording of the exact same thing. Watch the same prompt, same build."

Narrate over the recording exactly as scripted. The audience sees the output; you provide the commentary. Indistinguishable from live for most people.

**Recording checklist:**
- [ ] Recorded on a stable connection (not festival Wi-Fi)
- [ ] Full screen, high resolution
- [ ] Both builds captured: Prompt 1 + Plan Mode + Prompt 2
- [ ] No private data visible (no API keys, no personal files in terminal)
- [ ] Video saved locally — not streaming from cloud

---

### Layer 3 — Total Failure (recording fails too)
Nuclear option: walk through pre-built files.

**Before the event:** Save pre-built versions of both builds in `backup/`:
- `backup/phase1-pickleball-site/index.html` — the site after Prompt 1
- `backup/phase2-with-game/index.html` — the site after Plan Mode + Prompt 2

**Response:**
> "Technology is conspiring against me today. Fine — let me show you the end result instead."

*[Open backup HTML in browser]*

> "This is what Claude built when I ran this yesterday. The same prompt. Same output. Here's the site — [walk through it]."

Then show the game from the pre-built file. Narrate the process even though you're not building live.

This is the nuclear option but it's better than showing nothing.

---

## Day-Of Setup Checklist (Prevents 80% of Failures)

### Before leaving for the venue:
- [ ] Run both builds on home Wi-Fi — confirm they work
- [ ] Screen record the full run — save locally
- [ ] Save pre-built HTML files in `backup/`
- [ ] Kill all background processes (kills port conflicts)
- [ ] Test the backup recording plays correctly

### At the venue (30 min before):
- [ ] Connect to venue Wi-Fi — test Claude response time
- [ ] If Wi-Fi is slow: test if claude.ai browser works faster than Claude Code
- [ ] Have screen recording queued up, minimized, ready to switch to in 10 seconds
- [ ] Font size at 18–20pt minimum (readable from back row)
- [ ] Browser zoom at 125% for the preview window

### Known risk: Festival Wi-Fi
Festival networks are shared and unpredictable. Options:
1. **Phone hotspot** — most reliable fallback for Wi-Fi
2. **Pre-download** — Claude Code works offline for some tasks, but API calls need internet
3. **Screen recording** — the actual safety net

---

## Psychological Backup

Audiences at non-technical events are forgiving. They came to be inspired, not to evaluate your demo hygiene.

If something breaks and you handle it with confidence:
> "This is live coding — things break. The key is you're never blocked. You describe the problem, Claude fixes it."

...they remember the lesson, not the breakage.

The only unrecoverable failure is freezing or losing your thread. The script in `02-LIVE-BUILD-SCRIPT.md` has emergency lines for every scenario. Know them cold.
