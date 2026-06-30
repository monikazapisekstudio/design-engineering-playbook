# Copilot Instructions — design-engineering-playbook

This repository is a public AI-native design engineering playbook.
Skills, agents, and methodology for product design and engineering workflows.
No MCP, no external dependencies — everything is self-contained text.

## Repository map

| Folder | Contents |
|---|---|
| `skills/` | Reusable AI workflows — one `SKILL.md` per folder |
| `agents/` | Role-based AI agents — one `AGENT.md` per folder |
| `playbook/` | Long-form methodology |
| `rules/` | Operating guardrails |
| `commands/` | Repeatable agent actions |
| `prompts/` | Copy-paste prompt patterns |
| `doc-templates/` | Reusable project artifacts |

## How to use a skill or agent in Copilot Chat

Reference the file with `#file:` and then describe what you need:

```
#file:agents/agent-agile-master/AGENT.md
#file:agents/agent-agile-master/PERSONA.md
Act as this agent. I just finished a sprint and want to run a retrospective.
```

To load a specific skill on demand, add it to the same message:

```
#file:agents/agent-agile-master/skills/retrospective/SKILL.md
Run the retrospective skill for a solo practitioner.
```

---

## Available agents

### agent-agile-master (v1.3)

Agile master for solo practitioners with optional team-mode extensions.
Routes to 25+ rituals across 7 skills.

**Entry files:**
- `#file:agents/agent-agile-master/AGENT.md` — role, scope, ritual routing
- `#file:agents/agent-agile-master/PERSONA.md` — voice and hard rules

**Skills (load on demand, max 1 per session):**

| Skill | File | When |
|---|---|---|
| Ritual Router | `#file:agents/agent-agile-master/skills/ritual-router/SKILL.md` | "I don't know what to do next" |
| Sprint Planning | `#file:agents/agent-agile-master/skills/sprint-planning/SKILL.md` | Starting a sprint |
| Retrospective | `#file:agents/agent-agile-master/skills/retrospective/SKILL.md` | Ending a sprint |
| Workshop Facilitation | `#file:agents/agent-agile-master/skills/workshop-facilitation/SKILL.md` | Estimation, story mapping, discovery, BDD, customer interviews |
| Team Healer | `#file:agents/agent-agile-master/skills/team-healer/SKILL.md` | Team dysfunction, trust, toxic behavior |
| Metrics Strategist | `#file:agents/agent-agile-master/skills/metrics-strategist/SKILL.md` | OKR, OMTM, North Star Metric |
| Change Agent | `#file:agents/agent-agile-master/skills/change-agent/SKILL.md` | Agile adoption, ORID, information radiators |

**Sample prompts:**

```
#file:agents/agent-agile-master/AGENT.md #file:agents/agent-agile-master/PERSONA.md
New sprint. I have 12 backlog items and don't know which to pick.
```

```
#file:agents/agent-agile-master/AGENT.md
#file:agents/agent-agile-master/skills/retrospective/SKILL.md
Sprint just ended. Run a solo retrospective with me.
```

---

## Available skills (standalone)

### legible-agent-output

Force every user-facing string from an AI agent to be readable by a non-technical human. Replaces opaque codes (A127, ENOENT), framework jargon, and raw error strings with plain-language titles, status messages, and error descriptions.

```
#file:skills/legible-agent-output/SKILL.md
Rewrite this agent output for a non-technical product manager: [raw output]
```

Reference files (load when the skill asks for them):
- `#file:skills/legible-agent-output/references/articles-sources.md`
- `#file:skills/legible-agent-output/references/jargon-categories.md`
- `#file:skills/legible-agent-output/examples/before-after.md`

### kano-model-strategist

Classify features into Kano categories. Cut waste, build MDP over MVP.

```
#file:skills/kano-model-strategist/SKILL.md
Triage these 6 features for our SaaS product: [feature list]
```

Reference files (load when the skill asks for them):
- `#file:skills/kano-model-strategist/references/kano-classification.md`
- `#file:skills/kano-model-strategist/references/kano-vs-mdpmvp.md`
- `#file:skills/kano-model-strategist/references/experience-rot-checklist.md`
- `#file:skills/kano-model-strategist/references/ceo-pushback-scripts.md`

### socratic-dialogue

Reasoning rigor and anti-sycophancy guard. Use for high-stakes decisions and ambiguous requirements.

```
#file:skills/socratic-dialogue/SKILL.md
Apply socratic rigor to this architecture decision: [decision]
```

---

## Notes

- All content is public-safe. No secrets, no client data.
- Agent and skill files are plain Markdown — paste them directly into any AI chat if `#file:` is unavailable.
- For Claude Code CLI, see `agents/agent-agile-master/INSTALL.md` (Option A).
