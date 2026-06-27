# Handoff Instructions
**Canonical**: [KNOWLEDGE_ROOT]\knowledge\handoff-instructions.md
**Last Updated**: 2026-06-27

> This file tells every agent how to write a session handoff and where to save it.
> Read this at the end of every session before writing the handoff JSON.

---

## Purpose

A handoff JSON is written at the end of every session so the next context window can pick up exactly where we left off — without the user having to re-explain anything. The handoff is the memory bridge between sessions.

---

## Session Start Protocol

Every agent reads these files at the start of every session, before doing anything else:

1. `[KNOWLEDGE_ROOT]\knowledge\PROJECTS.md` — current project portfolio and status
2. `[KNOWLEDGE_ROOT]\knowledge\ROSTER.md` — active agents, roles, and routing
3. Latest handoff JSON from the agent's own `sessions\` folder

This is how the agent mesh stays current. No project or roster details are hardcoded in agent instructions — the live files are always the source of truth.

**Cross-agent context**: Any agent's `sessions\`, `memory\`, or `ideas\` folders can be read by any other agent when relevant. The full handoff structure lives at `[HANDOFFS_ROOT]\` — point any agent at any file to pull context across the mesh. Nothing is siloed. Everything is accessible.

---

## Handoff Folder Structure

Every agent gets a folder named after itself with three subfolders:

```
[HANDOFFS_ROOT]\[AGENT_NAME]\
    sessions\   <- handoff JSON files from every session
    memory\     <- long-term notes worth carrying forward permanently
    ideas\      <- ideas captured mid-session for future harvest
```

When a new agent is created, create a matching folder with all three subfolders. No routing table to maintain — the pattern is the rule.

---

## Naming Convention

### Session Handoffs
```
YYYY-MM-DD_[AGENT]_handoff.json
```

Multiple sessions on the same day: append `_v2`, `_v3`:
```
2026-05-28_HUSTLE_handoff.json
2026-05-28_HUSTLE_handoff_v2.json
```

### Memory Files
```
YYYY-MM-DD_memory.md
```

### Idea Files
```
YYYY-MM-DD_ideas.md
```

---

## Handoff JSON Structure

Every handoff must include these fields:

```json
{
  "timestamp": "YYYY-MM-DDTHH:MM:SSZ",
  "agent": "AGENT_NAME",
  "project": "Project or task name",
  "save_to": "[HANDOFFS_ROOT]\\[AGENT_NAME]\\sessions\\",
  "goal": "What this session was trying to accomplish",
  "current_status": "One sentence — where things stand right now",

  "progress": [
    "✅ Completed item",
    "✅ Completed item",
    "❌ Not yet done item"
  ],

  "immediate_next": [
    "First thing to do next session",
    "Second thing if applicable"
  ],

  "deferred": [
    "Item pushed out of this session scope — reason why"
  ],

  "open_questions": [
    "Question that needs the user's input — context on why it's blocking"
  ],

  "working_directory": "Absolute path to active project files",

  "technical_context": {
    "platform": "Claude Projects / Claude Code / Both",
    "current_issue": "Any blocker or open question",
    "what_works": "What is confirmed working",
    "next_step": "Specific next action"
  },

  "running_state": {
    "processes": [
      "dev server -- localhost:5173 -- kill: Ctrl+C in terminal / or 'none'"
    ],
    "open_branches": "branch name or 'none'",
    "open_worktrees": "path or 'none'",
    "git_status": "clean / dirty / uncommitted changes in [file]",
    "environment": "local / remote / both"
  },

  "verification": [
    "command or action -- expected outcome",
    "npm run dev -- dev server starts on localhost:5173 with no errors"
  ],

  "business_context": {
    "revenue_potential": "Why this matters commercially",
    "strategic_decisions": "Key decisions made this session",
    "constraints": "Anything that limits options"
  },

  "user_profile": {
    "name": "Your name",
    "communication_style": "How you prefer to communicate",
    "pace": "How fast you move through decisions",
    "what_works": "What landed well this session",
    "red_flags": "Anything that caused friction"
  },

  "agent_persona": {
    "tone": "How this agent communicates",
    "terminology": "Key terms used this session",
    "pace": "How decisions were made",
    "things_that_worked": "What to repeat",
    "things_to_avoid": "What not to repeat"
  },

  "failed_attempts": [],

  "session_friction": [],

  "assets_ready": [
    "Absolute path to file -- what it is / status"
  ],

  "ecosystem_changes": [
    "Any agents added, modified, or retired",
    "Any ROSTER.md or PROJECTS.md changes",
    "Any new handoff folders created"
  ],

  "priority": "HIGH / MEDIUM / LOW",

  "awakening_prompt": "Copy-paste ready prompt for the next session opening. Should include: what we were doing, what is done, what is next, and ask the user to confirm priority before proceeding."
}
```

---

## Field Notes

**`deferred` vs `open_questions`**: Deferred items are work pushed out by choice — scope, time, or priority. Open questions need the user's input before the next agent can move. Keep them separate. Don't bury either inside `immediate_next`.

**`running_state.processes`**: List every active process with its port and how to kill it. If nothing is running, write `"none"`. Never omit this field — the next agent cannot discover running processes on its own.

**`verification`**: One or two commands the next agent can run to confirm the environment is still healthy before touching anything. If there's nothing to verify (pure strategy session, no code), write `"none"`.

**`assets_ready`**: Absolute paths only. Relative paths break when the next agent has a different working directory.

---

## Memory File Format

At session end, if anything is worth carrying forward permanently, write a memory file:

```markdown
# [AGENT NAME] Memory
**Date**: YYYY-MM-DD
**Project**: Project name

## What to Remember
- Key decision or fact worth preserving long-term
- User preference discovered this session
- Pattern or principle that proved useful

## Context
Brief note on why this is worth keeping.
```

---

## Idea File Format

Any idea that surfaces mid-session — regardless of how half-baked — gets captured:

```markdown
# [AGENT NAME] Ideas
**Date**: YYYY-MM-DD
**Project**: Project name

## Ideas Captured

### [Idea Title]
**Source**: What triggered this idea
**Description**: What the idea actually is
**Potential**: Why it might be worth something later
**Status**: Raw / Needs research / Ready to pitch
```

---

## Awakening Prompt Format

The awakening prompt goes directly to the user after the handoff is saved. Format:

> I've reviewed the handoff from our last session. We were working on [task]. [What is complete]. [What is next]. Before I start: confirm this is still the priority, or let me know if something has changed.

---

## Two-Business Rule (if applicable)

If you operate multiple businesses that must stay separated, create a dedicated handoff folder per business and never cross-reference between them. The separation is absolute.

---

*Every agent reads this before writing a handoff. Every handoff is the memory bridge to the next session.*
