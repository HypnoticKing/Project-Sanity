# Project Sanity — Setup Instructions
> This file is read by Claude to set up Project Sanity on a new machine.
> If you're a human reading this — just tell Claude to read it and Claude will handle the rest.

---

## What You Are Doing

You are setting up Project Sanity — a session continuity and multi-agent coordination system for Claude.

When complete, the user will have:
- A knowledge folder with PROJECTS.md, ROSTER.md, and handoff-instructions.md
- A handoffs folder structure ready for agents
- Their first agent loaded and ready to use

---

## Step 1 — Ask the User for Their Paths

Ask the user two questions (one at a time):

1. Where do you want your knowledge folder to live?
   - Windows suggestion: `C:\Users\[name]\.claude\`
   - Mac/Linux suggestion: `~/.claude/`

2. Where do you want your handoffs folder to live?
   - Windows suggestion: `C:\Handoffs\`
   - Mac/Linux suggestion: `~/handoffs/`

Wait for both answers before proceeding.

---

## Step 2 — Create the Folder Structure

Create these folders on the user's machine:

```
[KNOWLEDGE_ROOT]\
    knowledge\
    agents\

[HANDOFFS_ROOT]\
```

---

## Step 3 — Copy and Configure the Knowledge Files

Copy these files from the repo into `[KNOWLEDGE_ROOT]\knowledge\`:
- `knowledge/PROJECTS.md`
- `knowledge/ROSTER.md`
- `knowledge/handoff-instructions.md`

Then replace all instances of `[KNOWLEDGE_ROOT]` and `[HANDOFFS_ROOT]` in every file with the actual paths the user provided.

---

## Step 4 — Walk the User Through PROJECTS.md

Open `[KNOWLEDGE_ROOT]\knowledge\PROJECTS.md` and ask the user:

> "Let's fill in your first project. What's the name of the main thing you're working on right now?"

Collect:
- Project name
- One sentence description
- Stack (technologies in use)
- Current status
- Working directory path

Write it into PROJECTS.md. Tell them they can add more projects any time by editing this file directly.

---

## Step 5 — Walk the User Through ROSTER.md

Open `[KNOWLEDGE_ROOT]\knowledge\ROSTER.md` and explain:

> "The roster is where you define your agents. You already have HUSTLE — a business partner and momentum agent — in the repo. Want to start with that one?"

If yes:
- Copy `agents/HUSTLE/agent.md` into `[KNOWLEDGE_ROOT]\agents\HUSTLE\agent.md`
- Replace all `[KNOWLEDGE_ROOT]` and `[HANDOFFS_ROOT]` placeholders with actual paths
- Add HUSTLE to ROSTER.md with its file path

If no:
- Ask what kind of agent they want first and help them create it

---

## Step 6 — Create the First Agent's Handoff Folders

For each agent set up in Step 5, create:

```
[HANDOFFS_ROOT]\[AGENT_NAME]\
    sessions\
    memory\
    ideas\
```

---

## Step 7 — Confirm and Hand Off

Tell the user:

> "Project Sanity is set up. Here's what was created:"

List everything that was created with full paths.

Then tell them:

> "To start your first session, paste the contents of [KNOWLEDGE_ROOT]\agents\HUSTLE\agent.md into a Claude Project as the system prompt. At the end of your session, ask Claude to write the handoff JSON to [HANDOFFS_ROOT]\HUSTLE\sessions\. Your next session will open with the awakening prompt and pick up exactly where you left off."

Then tell them one more thing:

> "Important: agents do not write handoffs automatically. You have to ask. On long sessions, don't wait until you're done — ask for a handoff before you step away, or mid-session if the conversation has been running deep. The context window has a limit, and once it's full, context is gone. A quick 'write the handoff' before you close the window is the habit that makes this whole system work."

---

## Notes for Claude

- Create folders one at a time and confirm each before moving to the next
- If any folder already exists, skip creation and continue
- If the user is on Windows, use backslashes in all paths
- If the user is on Mac or Linux, use forward slashes
- Do not move forward to the next step until the current step is confirmed complete
- If anything goes wrong, fix it before continuing

---

*Setup complete when the user has a working knowledge folder, at least one agent configured, and at least one handoff folder ready.*
