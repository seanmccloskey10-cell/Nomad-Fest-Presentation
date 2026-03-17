# Tool Decision — Claude Code vs Claude in Browser

---

## Recommendation: Claude Code

Use Claude Code. Here's why — and where the risk is.

---

## Claude Code

**Pros:**
- Files appear automatically — no copy-paste, no manual steps
- Can open a browser preview alongside the terminal (side by side = visual storytelling)
- The automation IS the wow — audience sees the machine build
- Plan Mode is a native feature, toggled cleanly with shift+tab
- More impressive to demonstrate: "I didn't even type the files, it just made them"

**Cons:**
- Terminal visible — looks intimidating to non-technical audiences
- Requires a project folder set up beforehand
- Port conflicts possible if background processes are running
- Slightly higher complexity if something breaks

**Mitigation for the terminal concern:**
Dedicate your screen layout so the browser preview is the dominant visual. Keep Claude Code small on the left, browser large on the right. Audience focuses on the output, not the terminal.

---

## Claude in Browser (claude.ai)

**Pros:**
- Familiar interface — looks like ChatGPT, less intimidating
- No setup needed — just open the tab
- Artifacts panel shows the site preview directly in the interface

**Cons:**
- Requires copy-pasting the generated code into a file or deploying manually
- Artifacts preview is small — harder to see from the back row
- Plan Mode framing is less clean (you'd have to explain it differently)
- Less impressive mechanically — feels like a chatbot, not a builder

---

## Decision Matrix

| Factor | Claude Code | Browser Claude |
|--------|------------|----------------|
| Wow factor | Higher | Lower |
| Wi-Fi dependency | Same | Same |
| Setup required | Yes | Minimal |
| Risk of failure | Slightly higher | Slightly lower |
| Audience perception | "A machine built it" | "He chatted with AI" |
| Plan Mode demo | Clean, native | Awkward to explain |

---

## Setup for Claude Code (Before the Event)

```bash
# Create clean project folder
mkdir pickle-palace
cd pickle-palace

# Open Claude Code
claude

# Pre-approve common commands to avoid permission popups during demo:
# In settings: write, edit, bash, open
```

**Screen layout:**
- Left side: Claude Code terminal (40% width)
- Right side: Browser preview (60% width)
- Font size: 18pt minimum in terminal, 125% zoom in browser

**Before going on stage:**
- [ ] Folder empty and ready
- [ ] Claude Code open on left
- [ ] Browser pointing to `localhost` or ready to open preview
- [ ] All background processes killed
- [ ] Prompts saved somewhere you can paste from instantly (Notes app, second monitor)

---

## Fallback: If Claude Code Won't Cooperate at the Venue

Switch to claude.ai Artifacts mid-session:

> "Let me switch to the browser version so you can see the output more clearly."

Paste Prompt 1 into claude.ai. It generates the HTML and shows a live preview in Artifacts. Less impressive mechanically but the output is the same.

This is acceptable. The output is still a working website from one prompt — the wow still lands.
