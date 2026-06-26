# Agent Mesh
### A session continuity and multi-agent coordination system for Claude

---

Most people re-explain their projects every time they open a new Claude session.

This system fixes that.

Agent Mesh is a lightweight framework that gives every Claude agent you build shared access to a live knowledge base — your projects, your roster, your decisions — so nothing gets lost between sessions and every agent starts informed.

Built and battle-tested over 18+ months of daily production use across a portfolio of AI products and automation systems.

---

## The Problem

Claude has no memory between sessions. Every new conversation starts cold.

Most workarounds look like this:
- Paste your project description at the top of every chat
- Re-explain what agent you want Claude to be
- Catch Claude up on what you decided last time
- Watch it make recommendations that ignore half your constraints

That's friction. It compounds. It slows everything down.

---

## The Solution: A Shared Knowledge Layer

Agent Mesh gives every agent three files to read at session start:

| File | What It Does |
|------|-------------|
| `PROJECTS.md` | Live portfolio — every project, its status, stack, and constraints |
| `ROSTER.md` | Agent hierarchy — who does what, when to route where |
| `handoff-instructions.md` | Session protocol — how to write handoffs, memory, and ideas |

No project details hardcoded in agent instructions. No roster details to update in ten places. One file changes, every agent is current next session.

That's the mesh.

---

## How Sessions Work

Every session ends with three outputs saved to the agent's handoff folder:

```
handoffs/
└── AGENT_NAME/
    ├── sessions/    <- handoff JSON -- full session state + awakening prompt
    ├── memory/      <- long-term notes worth carrying forward permanently
    └── ideas/       <- half-baked ideas captured mid-session for future harvest
```

Next session opens with the awakening prompt — a copy-paste ready brief that tells the agent exactly where you left off, what's done, and what's next. No re-explaining. No lost context.

The ideas folder is the sleeper feature. Every half-formed thought that surfaces mid-session gets captured instead of lost. Run a harvest pass later and something clicks.

**Nothing is siloed.** Any agent can read any other agent's sessions, memory, or ideas folders. Point an agent at any handoff file to pull context across the mesh.

---

## What's In This Repo

```
agent-mesh/
├── README.md
├── SETUP.md                         <- Claude reads this and sets up your machine
├── knowledge/
│   ├── PROJECTS.md                  <- template: your live project portfolio
│   ├── ROSTER.md                    <- template: your agent hierarchy
│   └── handoff-instructions.md      <- the full session protocol spec
├── agents/
│   ├── HUSTLE/
│   │   └── agent.md                 <- example: business partner + momentum agent
│   └── SCOUT/
│       └── agent.md                 <- example: repo triage and destiny engine
├── handoffs/
│   └── AGENT_NAME/
│       ├── sessions/
│       ├── memory/
│       └── ideas/
└── examples/
    ├── example-handoff.json         <- real handoff, fictional project
    └── example-project-brief.md     <- how to write a project brief agents can read
```

---

## Installation — Let Claude Do It

**1. Clone the repo**
```bash
git clone https://github.com/HypnoticKing/Project-Sanity.git
```

**2. Tell Claude to set it up**

Open a new Claude chat with filesystem access (Claude Desktop or Claude Code). Then paste this:

```
Read the SETUP.md file at [path to where you cloned the repo] and set up Agent Mesh on my machine.
```

Claude will:
- Ask where you want your knowledge folder and handoff folder to live
- Replace all placeholders with your actual paths
- Create your folder structure
- Walk you through filling in your first PROJECTS.md and ROSTER.md

That's it. First session starts informed.

---

## Manual Setup (if you prefer)

**1. Choose your paths**

Pick two folders on your machine:
- `KNOWLEDGE_ROOT` — where your knowledge files live (PROJECTS.md, ROSTER.md, agent files)
- `HANDOFFS_ROOT` — where session handoffs are saved

**2. Copy the knowledge files**

Copy everything from `knowledge/` into your `KNOWLEDGE_ROOT` folder.

**3. Fill in your projects and roster**

Open `PROJECTS.md` and add your active projects.
Open `ROSTER.md` and define your agents.

**4. Create your first agent**

Copy `agents/HUSTLE/agent.md` as a starting point. Replace the role, tone, and capabilities with your own. Keep the session start protocol — that's what connects the agent to the mesh.

**5. Create handoff folders**

For each agent, create:
```
[HANDOFFS_ROOT]/
└── YOUR_AGENT_NAME/
    ├── sessions/
    ├── memory/
    └── ideas/
```

**6. Run your first session**

Paste your agent's `agent.md` into a Claude Project as the system prompt. At the end of the session, ask Claude to write the handoff JSON and save it to `sessions/`.

Next session, paste the awakening prompt. You're back in context in seconds.

---

## The Agent Architecture

Agent Mesh works best with a clear hierarchy. The included agents show two patterns:

**HUSTLE** — a conversational Claude Projects agent. Lives in the chat window. Handles strategy, momentum, and decisions. Cannot touch files directly. Routes technical work elsewhere.

**SCOUT** — a Claude Code terminal agent. Has full filesystem access. Reads repos, writes reports, routes findings. Operates autonomously on command.

You can build as many agents as your workflow needs. The mesh keeps them coordinated.

---

## Key Principles

**One source of truth.** Projects and roster live in two files. Every agent reads them. Nothing gets out of sync.

**Agents are partners, not tools.** The best agents have a defined personality, clear scope, and patterns they watch for. They push back. They call things out. They give verdicts, not options.

**Momentum over perfection.** A shipped thing beats a perfect plan. The handoff system exists so you can stop mid-session and pick up tomorrow without losing an hour re-establishing context.

**Ideas are first-class output.** Half-formed ideas that surface mid-session are worth capturing. The ideas folder makes that effortless. A harvest pass across all agent idea folders is where unexpected connections happen.

**The awakening prompt is the secret.** A well-written awakening prompt means every session starts at full speed. It is not a summary — it is a launch pad.

**The mesh is open.** Every agent can read every other agent's handoffs, memory, and ideas. Context flows freely. Nothing is locked away.

---

## A Note on Agent Logic Drift

If you use AI coding agents to build or modify your projects, validate that their output aligns with your intent — not just that it runs.

AI agents can silently rewrite logic in ways that contradict your product's philosophy. The changes will look correct. The code will work. But the behavior will be wrong.

The fix: after any significant agent pass, review output against your original intent before shipping. Document your intent clearly in your project brief so agents have a standard to work against.

---

## Contributing

This is a living system. If you build agents, improve the handoff format, or find better patterns — PRs are welcome.

---

## License

MIT. Use it, adapt it, build on it.

---

*Built by someone who got tired of re-explaining everything. Shared because nobody else should have to either.*
