# Agent Roster
**Canonical**: [KNOWLEDGE_ROOT]\knowledge\ROSTER.md
**Last Updated**: YYYY-MM-DD

> Single source of truth for all agents in your ecosystem.
> Every agent reads this file at session start to understand who does what.
> Update this file when agents are created, versioned, or retired.

---

## Hierarchy

Define your agent hierarchy here. Example structure:

```
CHIEF_AGENT (sits above all — strategy, architecture, coordination)
├── AGENT_A   — Role description
├── AGENT_B   — Role description
└── AGENT_C   — Role description
    ├── SPECIALIST_A  — Narrow role, created when needed
    └── SPECIALIST_B  — Narrow role, created when needed
```

---

## Active Agents

### [AGENT NAME]
- **Role**: What this agent does and when to use it
- **Status**: Active (vX.X.X)
- **Handoff folder**: Path to this agent's handoff folder
- **Agent file**: Path to this agent's instructions file
- **Commission when**: Specific trigger conditions for routing work to this agent

---

### [AGENT NAME]
- **Role**: What this agent does and when to use it
- **Status**: Active (vX.X.X)
- **Handoff folder**: Path to this agent's handoff folder
- **Agent file**: Path to this agent's instructions file
- **Commission when**: Specific trigger conditions for routing work to this agent

---

## Agents Not Yet Built

| Agent | Role | Create When |
|-------|------|-------------|
| [Name] | Brief role description | Trigger condition |
| [Name] | Brief role description | Trigger condition |

---

## Roster Status Summary

| Agent | Status | File |
|-------|--------|------|
| [Agent Name] | Active vX.X.X | agents\[NAME]\agent.md |
| [Agent Name] | Not Built | - |

---

*Update this file when agents are added, versioned, or retired. Agents read it — never overwrite it.*
