# Project Sanity
### A session continuity and multi-agent coordination system for Claude

---

Most people re-explain their projects every time they open a new Claude session.

This system fixes that.

Project Sanity is a lightweight agent mesh framework that gives every Claude agent you build shared access to a live knowledge base — your projects, your roster, your decisions — so nothing gets lost between sessions and every agent starts informed.

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

Project Sanity gives every agent three files to read at session start:

| File | What It Does |
|------|-------------|
| `PROJECTS.md` | Live portfolio — every project, its status, stack, and constraints |
| `ROSTER.md` | Agent hierarchy — who does what, when to route where |
| `handoff-instructions.md` | Session protocol — how to write handoffs, what to capture, how to wake up |

No project details hardcoded in agent instructions. No roster details to update in ten places. One file changes, every agent is current next session.

That's the mesh.

---

## The Part That Makes People Stop

Here's what most people don't realize is possible:

A **Claude Projects agent** (chat window) and a **Claude Code agent** (terminal) can share the same state — because the shared truth isn't inside Claude. It's on your disk.

Both agents read the same `PROJECTS.md` and `ROSTER.md`. Both write handoffs to the same folder structure. So when you say to any agent — Projects or Code — "check what [Agent X] was working on in the last session," it navigates to that agent's handoff folder and reads it.

The mesh isn't agents talking to each other in real time. It's agents sharing a persistent, readable, writable state on disk that any of them can access at any time.

You can be in a conversation with a Projects agent in the chat window while a Code agent is writing files to disk — and they're sharing the same picture of your work.

That's the architecture. One source of truth. Every agent current. Nothing siloed.

---

## How Sessions Work

Every session ends with three outputs saved to the agent's handoff folder:

```
[HANDOFFS_ROOT]/
└── AGENT_NAME/
    ├── sessions/    ← handoff JSON — full session state + awakening prompt
    ├── memory/      ← long-term notes worth carrying forward permanently
    └── ideas/       ← half-baked ideas captured mid-session for future harvest
```

The next session opens with the awakening prompt — a copy-paste ready brief that tells the agent exactly where you left off, what's done, and what's next. No re-explaining. No lost context.

Any agent can read any other agent's `sessions/`, `memory/`, or `ideas/` folders. Point any agent at any handoff file to pull context across the mesh. Nothing is siloed. Everything is accessible.

### What a Handoff Actually Captures

A handoff is not a summary. It's a full environment snapshot:

- **Progress** — what's done, what's not
- **Immediate next** — exactly where to pick up
- **Running state** — every active process, its port, how to kill it
- **Verification** — commands to confirm the environment is healthy before touching anything
- **Deferred items** — work pushed out by choice, and why
- **Open questions** — things that need your input before the next agent can move
- **Awakening prompt** — copy-paste ready, drops the next session straight into context

See `examples/example-handoff.json` for a real handoff with all fields populated.

### A Critical Note on Timing

Agents do not write handoffs automatically. Claude has no background process watching your session. If the context window fills before you ask for a handoff, context is lost.

The fix is simple: ask for the handoff before you're done, not after.

Two habits that work:
- **Before stepping away** — any time you say you're leaving or wrapping up, ask for the handoff in the same message
- **During long sessions** — ask for an interim handoff mid-session. The cost is low. The cost of a lost context window is not.

Well-configured agents offer handoffs proactively at milestones and pauses. You shouldn't have to remember — but until an agent is set up that way, the habit is yours to build.

---

## What's In This Repo

```
project-sanity/
├── README.md                        ← you are here
├── SETUP.md                         ← read this to get set up (Claude does it for you)
├── knowledge/
│   ├── PROJECTS.md                  ← template: your live project portfolio
│   ├── ROSTER.md                    ← template: your agent hierarchy
│   └── handoff-instructions.md      ← the full session protocol spec
├── agents/
│   └── AGENT-BUILDER/
│       └── agent.md                 ← builds, validates, and upgrades agents
├── handoffs/
│   └── AGENT_NAME/
│       ├── sessions/
│       ├── memory/
│       └── ideas/
└── examples/
    ├── example-handoff.json         ← real handoff, fictional project
    └── example-project-brief.md     ← how to write a project brief agents can read
```

---

## Getting Started

**1. Clone the repo**

```bash
git clone https://github.com/HypnoticKing/Project-Sanity.git
```

**2. Tell Claude to set it up**

Open Claude Desktop (or any Claude session with filesystem access). Paste this:

```
Read the SETUP.md file at [path to where you cloned the repo] and set up Project Sanity on my machine.
```

Claude becomes the Setup Agent. It will:
- Ask where you want your knowledge and handoffs folders to live
- Create your folder structure
- Copy and configure your knowledge files
- Walk you through your first project entry
- Import any existing agents you want to bring into the mesh
- Set up your first agent
- Hand off to the Agent Builder if you want to create something new

That's it. You don't touch a config file. You don't edit anything manually. You just answer questions.

---

## The Agent Builder

Once you're set up, the Agent Builder is your main tool for growing the mesh.

**Three things it does:**

**Build** — Tell it what you need in plain English. It interviews you, then produces a complete, mesh-ready agent file — already wired to your knowledge layer, already following the handoff protocol, already registered in your roster.

**Check + fix** — Paste any agent you've already written. It runs a mesh compliance check across five criteria and patches only what's missing. Your existing file stays intact.

**Register** — Have an agent you just want tracked in the system without changing? It adds it to your roster and creates its handoff folders.

You focus on what you want your agents to do. The Builder handles how they work together.

To use the Agent Builder any time:

```
Read [KNOWLEDGE_ROOT]/agents/AGENT-BUILDER/agent.md and help me build an agent.
```

---

## The Agent Architecture

Project Sanity works best with a clear hierarchy. A simple example:

```
STRATEGIST    (conversational — Claude Projects)
├── BUILDER   (file-aware — Claude Code)
└── WRITER    (conversational — Claude Projects)
```

The Strategist handles decisions and direction in chat. The Builder executes technical work in the terminal with filesystem access. The Writer handles drafts and edits in chat. All three share the same knowledge layer and handoff folders. Any one of them can check what the others were working on.

Your roster will look different. The mesh adapts to whatever hierarchy makes sense for your work.

---

## Key Principles

**One source of truth.** Projects and roster live in two files. Every agent reads them. Nothing gets out of sync.

**You focus on what. The system handles how.** Agents are built to work together. You don't wire them manually — the Builder does it. You don't teach each new agent your whole project history — the knowledge layer does it.

**Agents are partners, not tools.** The best agents have a defined personality, clear scope, and patterns they watch for. They push back. They call things out. They give verdicts, not options.

**Momentum over perfection.** A shipped thing beats a perfect plan. The handoff system exists so you can stop mid-session and pick up tomorrow without losing an hour re-establishing context.

**Ideas are first-class output.** Half-formed ideas that surface mid-session are worth capturing. The ideas folder makes that effortless. A harvest pass across all agent idea folders is where unexpected connections happen.

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
