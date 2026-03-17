# Dry Run Guide — Nomad Fest

**For practice runs before the event.**

---

## What a Good Dry Run Looks Like

Run the full 20 minutes as if you're on stage. No pausing, no stopping to fix things. Simulate the real constraints:

- Wi-Fi only (no localhost shortcuts)
- Prompts copy-pasted from `PROMPTS.md` — not retyped
- Browser preview open on the right, Claude Code on the left
- Font size as it will appear on the projected screen

After each run: update `LESSONS-LEARNED.md` with what worked and what didn't.

---

## Before Each Dry Run

```bash
# Clean the project folder
rm -f index.html
rm -rf *.html

# Kill background processes
taskkill /F /IM node.exe /T 2>nul || echo "No node processes"

# Verify Claude Code opens cleanly
claude
```

- [ ] Project folder empty (clean slate)
- [ ] Claude Code open — no previous context
- [ ] Browser ready but not pointing at anything yet
- [ ] Prompts open in a Notes app or second monitor for fast pasting
- [ ] Screen recording running (to review afterward)

---

## The Run

### Segment 1 — Build #1 (target: under 2 min from prompt → browser open)

1. Paste Prompt 1
2. Hit enter — start a stopwatch
3. When Claude finishes: open preview in browser
4. Record the time

**Target:** File written and browser open within 90 seconds of hitting enter.

**If it takes over 3 minutes:** Wi-Fi is too slow. Practice the narration to fill the time naturally, or test on hotspot.

---

### Segment 2 — Plan Mode + Build #2 (target: plan visible within 30 sec, build done within 5 min)

1. Enable Plan Mode (shift+tab)
2. Paste Prompt 2
3. Hit enter — watch for plan output
4. When plan appears: practice reading 2–3 items out loud
5. Approve the plan
6. When build finishes: scroll to game section, click Play

---

## After Each Dry Run — LESSONS-LEARNED.md

Update immediately while it's fresh.

**Questions to answer:**
- How long did Build #1 actually take?
- Did the site look good at presentation zoom (125% browser, 18pt font)?
- Did Plan Mode output something worth pointing at?
- Did the game work first try?
- What felt awkward or rushed?
- What line got the best reaction?

---

## Success Metrics Per Run

| Metric | Target |
|--------|--------|
| Build #1 time (prompt → browser open) | Under 90 seconds |
| Plan Mode time (prompt → plan visible) | Under 45 seconds |
| Build #2 time (approve → game working) | Under 4 minutes |
| Game works on first play | Yes |
| No permission popups | Yes |
| Narration felt natural (not scripted) | Yes |

---

## Ready for the Event When:

- [ ] Both builds work consistently across 3+ dry runs
- [ ] Build #1 is under 90 seconds on festival-grade Wi-Fi (or hotspot)
- [ ] Screen recording saved as `backup/demo-recording.mp4`
- [ ] Pre-built HTML files saved in `backup/`
- [ ] You've said the narration out loud enough times it feels off-the-cuff
