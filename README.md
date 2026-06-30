# Design Engineering Playbook

AI-assisted workflow artefacts for product designers working in agile and lean environments. Agents, skills, and design engineering tools built for AI-native workflows across the full product lifecycle.

## Installation

**Claude Code / Codex CLI / Cursor** — install all skills and agents with one command:

```bash
npx skills add monikazapisekstudio/design-engineering-playbook
```

**GitHub Copilot** — available via [awesome-copilot](https://github.com/github/awesome-copilot):
- [Agent Agile Master](https://github.com/github/awesome-copilot/pull/2051) (PR pending)
- [Kano Model Strategist + Socratic Dialog](https://github.com/github/awesome-copilot/pull/2053) (PR pending)

**Cursor** — copy the `.cursor/` folder from this repo into your project root:
- `.cursor/skills/` — skills (kano-model-strategist, socratic-dialogue, legible-agent-output)
- `.cursor/agents/` — agents (agent-agile-master)

Skills and agents activate automatically when Cursor detects a relevant task.

**Manual install** — copy any `SKILL.md` or `AGENT.md` file into your project and reference it in your agent config.

---

## Vision

The goal is to help senior designers:

- use AI to build strategy and manage projects faster
- create advanced AI ecosystems for ideating and running product work
- close the gap between design and development
- learn to code applications efficiently with AI-assisted workflows
- how can build applications with AI without falling into chaos
- design, edit, and govern design systems across software
- keep design tokens, components, documentation, and code aligned
- use cutting-edge integrations and deployment tools in daily workflows
- turn real project work into reusable frameworks, checklists, and case studies

## Current status

This repository is an early public MVP.

The playbook will grow over time.

## Author

Created by Monika Zapisek, Product Designer / Design Engineer / monikazapisek.com

I work across product design, UX strategy, design systems, designOps, AI-assisted workflows, and frontend implementation.

## History

* **2026-06-30** — Added legible-agent-output skill (v1.0) to skills/. Replaces opaque codes (A127, ENOENT), framework jargon (`cycle 2 dispatch`, `Phase 2: post-merge validation`), raw error strings, and bare percentages with plain-language titles, status messages, and error descriptions. The skill carries 7 laws, a 6-category failure-mode taxonomy, 30+ worked before/after transformations, and a 3-prompt eval loop. Grounded in 6 published UX articles (Smashing Magazine, Hatchworks, Exalt Studio, boost.ai, Orange Loops, Medium Bootcamp), all verified on 2026-06-30 — see `references/articles-sources.md`. Includes ATTRIBUTION.md, EVIDENCE.md (Path B eval), SYNCHRONIZATION.md, LICENSE (MIT). Designed as a cross-cutting rule for any agent that emits user-facing strings; pairs with the 5 workspace agents already in the playbook (agent-agile-master, agent-career-growth, agent-dev-lead, agent-marketing, agent-publisher, agent-strategic-pm).
* **2026-06-15** — Added kano-model-strategist skill (v1.1.0) to skills/. The skill classifies features into Kano categories (Must-be / Performance / Attractive / Indifferent / Reverse / Questionable) and prunes the backlog to prevent Experience Rot. v1.1 adds T-shirt sizing rubric, CEO pushback scripts (4 patterns), and a market-access vs. user-facing feature distinction. Includes EVIDENCE.md (5-point Path B eval). Licensed under MIT.
* **2026-06-06** — Added socratic-dialogue skill (v2.3) to skills/. The skill enforces reasoning rigor via a 5-step Socratic workflow, with anti-bias, anti-sycophancy, and Cognitive Immune System framing. Licensed under MIT.
