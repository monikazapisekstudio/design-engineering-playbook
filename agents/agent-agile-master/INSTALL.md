---
created: 2026-06-18
updated: 2026-06-18
version: 1.3
description: Installation guide for agent-agile-master (v1.3 — Working Genius, Toxic Behavior Playbook, Prime Directive, Copilot option added)
---

# Installation Guide — agent-agile-master

Agile master for solo practitioners, with optional team-mode extensions.
Works with Claude Code CLI, Claude.ai, and GitHub Copilot Chat.

---

## Option A — Claude Code CLI (recommended)

Claude Code automatically discovers agents placed in `.claude/agents/`.

### Step 1: Download the agent

Clone or download the `agent-agile-master/` folder into your project.

### Step 2: Create the agent file

Create `.claude/agents/agent-agile-master.md` in your project root with this content:

```markdown
---
name: agent-agile-master
description: Agile master for solo practitioners with optional team-mode. Routes to 25+ rituals across 7 skills: sprint planning, retrospective, quarterly OKR review, estimation, story mapping, discovery (Torres OST), outcomes vs outputs, build trap, BDD/ATDD, customer interview, team health, OKR planning, OMTM, change management, ORID, information radiators. Use when starting/ending a sprint, planning a quarter, encountering team dysfunction, or adopting new process.
model: claude-sonnet-4-6
---

[paste the contents of AGENT.md here]
```

### Step 3: Place skills (optional but recommended)

Copy the `skills/` folder alongside your agent file so Claude Code can load
procedures on demand:

```
your-project/
└── .claude/
    └── agents/
        └── agent-agile-master.md   ← agent entry point
your-project/ (or anywhere Claude Code can read)
└── agent-agile-master/
    └── skills/                     ← 7 skills, loaded on demand
        ├── ritual-router/SKILL.md
        ├── sprint-planning/SKILL.md
        ├── retrospective/SKILL.md
        ├── workshop-facilitation/SKILL.md
        ├── team-healer/SKILL.md
        ├── metrics-strategist/SKILL.md
        └── change-agent/SKILL.md
```

### Step 4: Invoke

```
@agent-agile-master nowy sprint, co robimy?
@agent-agile-master koniec sprintu, czas na retro
@agent-agile-master ile to zajmie? (estimation)
@agent-agile-master quarterly OKR review
@agent-agile-master zespół nie działa, brak zaufania
@agent-agile-master mam za dużo metryk
@agent-agile-master pivotuję produkt, jak to ogłosić
@agent-agile-master mam trudną rozmowę 1:1
```

Or just describe your situation — Claude Code will route automatically when
the description matches.

---

## Option B — Claude Desktop / Cowork

If you have the agent files in your connected workspace folder, tell Claude at
the start of the session:

> "Load agent-agile-master and follow its rules"

Claude will read the files directly from your folder. No copying needed.

## Option E — OpenAI Codex CLI

Codex CLI automatically reads `AGENTS.md` from the repo root, so it gets
repo context without any setup. Load the full agent by telling Codex which
files to read.

### Step 1: Clone or download the repo

```bash
git clone https://github.com/monikazapisekstudio/design-engineering-playbook
cd design-engineering-playbook
```

### Step 2: Run Codex from the repo root

Codex reads `AGENTS.md` automatically. To load the full agent:

```bash
codex "Read agents/agent-agile-master/AGENT.md and agents/agent-agile-master/PERSONA.md, then act as that agent. New sprint, 12 backlog items, don't know which to pick."
```

### Step 3: Load a skill on demand

```bash
codex "Read agents/agent-agile-master/AGENT.md, agents/agent-agile-master/PERSONA.md, and agents/agent-agile-master/skills/retrospective/SKILL.md. Act as the agent and run a solo retrospective with me."
```

### Sample entry prompts

```bash
# Ritual routing
codex "Read agents/agent-agile-master/AGENT.md agents/agent-agile-master/PERSONA.md agents/agent-agile-master/skills/ritual-router/SKILL.md — act as the agent. I don't know what to do next. I finished some tasks, I have a backlog."

# Sprint planning
codex "Read agents/agent-agile-master/AGENT.md agents/agent-agile-master/PERSONA.md agents/agent-agile-master/skills/sprint-planning/SKILL.md — act as the agent. Starting a new sprint."
```

### Notes

- Run Codex from the repo root so relative file paths resolve correctly.
- No MCP, no plugins — all skills are plain text files.
- `extends:` in frontmatter is ignored by Codex (no error, no effect).
- `AGENTS.md` in the repo root is read automatically — it indexes available agents and skills.

---

## Option D — GitHub Copilot Chat (VS Code)

No installation needed. GitHub Copilot reads files directly from your workspace
when you reference them with `#file:`.

### Step 1: Open Copilot Chat in agent mode

In VS Code: open Copilot Chat panel → switch to **Agent** mode (the `@` icon or
the mode selector at the bottom of the chat input).

### Step 2: Open the repo as your workspace

`File → Open Folder` → select `design-engineering-playbook/`. The `#file:` paths
must resolve relative to the open workspace root.

### Step 3: Load the agent

```
#file:agents/agent-agile-master/AGENT.md
#file:agents/agent-agile-master/PERSONA.md
Act as this agent. [describe your situation]
```

### Step 4: Load a skill on demand

```
#file:agents/agent-agile-master/skills/retrospective/SKILL.md
Run the retrospective skill.
```

### Sample entry prompts

```
#file:agents/agent-agile-master/AGENT.md #file:agents/agent-agile-master/PERSONA.md
New sprint. I have 12 backlog items, don't know which to pick.
```

```
#file:agents/agent-agile-master/AGENT.md #file:agents/agent-agile-master/PERSONA.md
#file:agents/agent-agile-master/skills/ritual-router/SKILL.md
I don't know what to do next. I finished some tasks, I have a backlog.
```

### Notes

- Copilot does not auto-discover agents — reference files manually each session.
- `extends:` in frontmatter is ignored by Copilot (no error, no effect).
- All skills are MCP-free and require no plugins.
- Copilot may prepend a task-planning step before responding — this is Copilot-native behavior, not the agent. The agent response follows after.
- For workspace-level auto-context, see `.github/copilot-instructions.md` in this repo.

---

## Option C — Claude.ai web or mobile

Use **Projects** for persistent setup:

1. Open or create a Project in Claude.ai
2. Go to Project instructions
3. Paste the full contents of `AGENT.md` (and optionally `PERSONA.md`)
4. Every conversation in that project starts with the agent loaded

Or paste inline at the start of any conversation:

> "Act as the agent described below: [paste AGENT.md contents]"

Then load skills on demand by pasting the relevant `SKILL.md` when needed.

---

## What's included

| File | Purpose |
|---|---|
| `AGENT.md` | Role, scope, 25+ rituals, decision logic |
| `PERSONA.md` | Voice, hard rules, communication style |
| `skills/ritual-router/SKILL.md` | Which ceremony to run when |
| `skills/sprint-planning/SKILL.md` | Sprint planning ceremony |
| `skills/retrospective/SKILL.md` | Retrospective + quarterly OKR review |
| `skills/workshop-facilitation/SKILL.md` | 8 workshops (estimation, story mapping, discovery, outcomes, BDD, interviews) |
| `skills/team-healer/SKILL.md` | Team health, hoarders, psych safety, sheepdog |
| `skills/metrics-strategist/SKILL.md` | OKR, OMTM, NSM, metrics audit |
| `skills/change-agent/SKILL.md` | Kotter, ORID, information radiators |
| `ATTRIBUTION.md` | Framework citations and sources (15+ books) |
| `EVIDENCE.md` | Quality gates, evidence base, risk notes |

---

## Requirements

- Claude Sonnet or better (claude-sonnet-4-6 recommended)
- Claude Code CLI (for Option A) — [docs.anthropic.com](https://docs.anthropic.com)
- No external dependencies — agent runs entirely on text

---

## Knowledge sources

The agent references these books and courses when facilitating rituals.
You don't need to own them — the agent has built-in knowledge of the frameworks.
They're listed here for attribution and deeper learning:

**Books (agile / scrum foundations):**
- *User Story Mapping* — Jeff Patton (O'Reilly, 2014) ISBN 978-1491904893
- *Continuous Discovery Habits* — Teresa Torres (Product Talk, 2021) ISBN 978-1736633304
- *Lean UX* — Gothelf & Seiden (O'Reilly, 2021) ISBN 978-1098116309
- *Inspired* — Marty Cagan (Wiley, 2017) ISBN 978-1119387503
- *Agile Estimating and Planning* — Mike Cohn (Prentice Hall, 2005) ISBN 978-0131479418
- *The Five Dysfunctions of a Team* — Patrick Lencioni (Jossey-Bass, 2002) ISBN 978-0787960759
- *Fearless Organization* — Amy Edmondson (Wiley, 2018) ISBN 978-1119477242
- *Radical Focus* — Christina Wodtke (Self-published, 2016) ISBN 978-0996006001
- *Measure What Matters* — John Doerr (Portfolio, 2018) ISBN 978-0525536222
- *Escaping the Build Trap* — Melissa Perri (O'Reilly, 2018) ISBN 978-1491973790
- *Lean Analytics* — Croll & Yoskovitz (O'Reilly, 2013) ISBN 978-1449335670
- *Lean Startup* — Eric Ries (Crown Business, 2011) ISBN 978-0307887894
- *Specification by Example* — Gojko Adzic (Manning, 2011) ISBN 978-1617291634
- *ATDD by Example* — Howard Podeswa (Addison-Wesley, 2012) ISBN 978-0321784155
- *The Mom Test* — Rob Fitzpatrick (Self-published, 2013) ISBN 978-1492180746
- *Leading Change* — John Kotter (Harvard Business Review Press, 1996) ISBN 978-0875847474
- *Switch* — Chip & Dan Heath (Broadway Books, 2010) ISBN 978-0385528757
- *Nonviolent Communication* — Marshall Rosenberg (PuddleDancer Press, 2003) ISBN 978-1892005281

**Online courses** (Mountain Goat Software — mountaingoatsoftware.com):
- Agile Estimating and Planning
- Better Retrospectives
- Better User Stories
- Estimating With Story Points
- Scrum Repair Guide
- Retrospectives Repair Guide

**Free online resources:**
- North Star Playbook (Amplitude, 2018) — northstar.playbook.amplitude.com
- Retromat (retromat.org) — free retrospective activity planner

---

## License

MIT — see [LICENSE](./LICENSE). Free to use, modify, and distribute.
