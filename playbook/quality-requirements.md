# Quality Requirements for Skills & Agents

**Owner:** Monika Zapisek / Design Engineering Playbook
**Created:** 2026-06-18
**Status:** Active — applies to all current and future skills/agents in this repo
**Related:** `playbook/distribution/strategy-and-roadmap.md` §4.2 (frontmatter contract), `agents/agent-agile-master/DOD-CHECKLIST.md` (per-asset gates)

---

## Purpose

This document is the **acceptance contract** for any skill or agent published under the
Design Engineering Playbook. It exists so that:

1. **PR reviewers** (awesome-copilot, internal team) can check claims against a stable rule set.
2. **New asset authors** know up front what "done" looks like before they start writing.
3. **Distribution channels** (awesome-copilot, Cursor, VS Code Agent Plugins, GitHub Copilot,
   Claude Code, Codex) get assets that satisfy a consistent bar — no per-channel surprises.
4. **Refactors** (Copilot refactor 2026-06-18 being the case in point) have an explicit
   "Tested with" / "Designed for" test instead of ad-hoc decisions.

If any requirement below is violated, the asset must either be fixed or have an explicit
exception recorded in §6 of `playbook/distribution/strategy-and-roadmap.md`.

---

## Functional Requirements (FR) — what the asset MUST do

| ID    | Requirement                                                                                                            | When checked   |
|-------|------------------------------------------------------------------------------------------------------------------------|----------------|
| FR-1  | Skill has one clear `job` (single responsibility). No Swiss-Army-knife skills.                                          | PR review      |
| FR-2  | Frontmatter contains `name` + `description` with explicit **"use when"** trigger phrases AND **"do NOT use"** guard phrases. | automated lint |
| FR-3  | Skill reads `references/` in declared priority order; does **not** duplicate their content into the main `SKILL.md`.   | manual review  |
| FR-4  | Agent orchestrator lists every ritual it can run + the trigger condition ("kiedy co") for each.                        | manual review  |
| FR-5  | Every skill ships `ATTRIBUTION.md` (sources) and `EVIDENCE.md` (tests, edge cases, token budget, quality gates).       | manual review  |
| FR-6  | `description:` trigger phrases are tested against ≥ 5 real user queries before merge; results recorded in `EVIDENCE.md`.| PR review      |

---

## Non-Functional Requirements (NFR) — how the asset MUST behave

| ID     | Category            | Requirement                                                                                                    |
|--------|---------------------|----------------------------------------------------------------------------------------------------------------|
| NFR-1  | Interop             | Frontmatter contract per `playbook/distribution/strategy-and-roadmap.md` §4.2 — `Tested with` vs `Designed for` distinction enforced. |
| NFR-2  | Interop             | No MCP deps / no external services unless explicitly declared in frontmatter and justified in `EVIDENCE.md`.   |
| NFR-3  | Portability         | Asset runs standalone — no hidden references to private `.agents/`, monorepo-only paths, or unwired env vars.   |
| NFR-4  | Performance         | Activation cost bounded: skill `description` ≤ 1 kB; full `SKILL.md` ≤ 50 kB; total bundled assets ≤ 5 MB.     |
| NFR-5  | License             | Every asset is MIT + carries clear `author` + `project` attribution in frontmatter and README.                  |
| NFR-6  | Reliability         | Smoke test in every claimed runtime (Copilot, Claude Code, Codex, VS Code…) — evidence file in `integrations/`.|
| NFR-7  | Maintainability     | Semver in frontmatter (`version: x.y[.z]`); CHANGELOG entry for every breaking change.                         |
| NFR-8  | Discoverability     | Root `README.md` skill/agent index updated on add/remove; keywords/tags consistent across frontmatter + README. |
| NFR-9  | Adversarial safety  | High-stakes skills (Kano pruning, Story Map verification, socratic-dialogue) implement anti-fluency + anti-sycophancy guard. |
| NFR-10 | Documentation       | `DOD-CHECKLIST.md` fully ticked before merge; PR description links the checklist + smoke-test evidence.         |

---

## Business Rules (BR) — hard constraints on the project

| ID   | Rule                                                                                                                                                                |
|------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| BR-1 | New skill MUST NOT duplicate an existing one — author must search `skills/` and `agents/` before creating and document the gap in the new asset's `EVIDENCE.md`.    |
| BR-2 | License is MIT for all new assets (decision recorded 2026-06-18, see §7 of strategy-and-roadmap). Re-licensing an existing asset follows the same sole-author process.|
| BR-3 | Author = **Monika Zapisek**, Project = **Design Engineering Playbook**. Dual-brand rule: byline = person, container = project.                                    |
| BR-4 | `Designed for:` = intent claim (planned target). `Tested with:` = fact (actually validated). Both come from §4.2 of `strategy-and-roadmap.md`.                    |
| BR-5 | Release = merge to `main` + version bump in frontmatter + CHANGELOG entry + root README index update. No silent releases.                                         |
| BR-6 | Sprint commitments honor the Definition of Done from §8 of `strategy-and-roadmap.md` before any "Day done" / sprint review.                                         |

---

## Quality Gates (acceptance criteria per release)

Every release — whether a new asset, a version bump, or a re-license — must satisfy **all** of these before merge:

- [ ] **Frontmatter contract** (§4.2) — automated lint passes (name, description, license, model, compatibility, metadata)
- [ ] **Smoke test in every claimed runtime** — manual evidence file linked from `EVIDENCE.md` (e.g. `integrations/copilot-smoke-test.md`)
- [ ] **DOD-CHECKLIST.md fully ticked** — manual review by author + reviewer
- [ ] **CHANGELOG / version bump** — frontmatter `version:` updated, `CHANGELOG.md` (or equivalent) entry added for breaking changes
- [ ] **README index current** — root `README.md` skill/agent list reflects the new state
- [ ] **License + author + project header everywhere** — `LICENSE`, `README.md`, frontmatter, and PR description all carry the same attribution

---

## How to use this document

| Audience           | Use case                                                                                       |
|--------------------|------------------------------------------------------------------------------------------------|
| Asset author       | Read before starting a new skill/agent; self-check against FR/NFR/BR before opening PR.        |
| PR reviewer        | Walk through Quality Gates checklist; reject if any box unchecked.                              |
| Distribution owner | Confirm channel-specific format (e.g. awesome-copilot CONTRIBUTING.md) does not violate NFR-1. |
| External reviewer  | Cite FR/NFR IDs when asking "why this claim?" — keeps feedback structured.                     |

---

## Change log

| Date       | Change                                                                                              |
|------------|-----------------------------------------------------------------------------------------------------|
| 2026-06-18 | Initial version. 6 FR, 10 NFR, 6 BR, 6 quality gates. Anchored in the Copilot refactor smoke test (2026-06-18) that motivated NFR-6. |