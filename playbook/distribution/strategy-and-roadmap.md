# Distribution Strategy & Roadmap

**Owner:** Monika Zapisek / Design Engineering Playbook
**Created:** 2026-06-18
**Status:** Active — Sprint 0 (inventory + Kano + strategy)

---

## 1. Inventory (what we actually have)

| Asset | Type | License | Location | Quality |
|---|---|---|---|---|
| `kano-model-strategist` | Standalone skill | MIT | `skills/kano-model-strategist/` | Production-ready (182 lines, references/, version 1.1, full frontmatter) |
| `agent-agile-master` | Agent orchestrator + 4 nested skills | MIT | `agents/agent-agile-master/` | Production-ready (AGENT.md, PERSONA.md, EVIDENCE.md, ATTRIBUTION.md, SYNCHRONIZATION.md, 4 skills, full frontmatter) |
| `socratic-dialog` | Standalone skill (imported) | MIT (relicensed 2026-06-18 from CC-BY-4.0 → MIT) | `skills/socratic-dialog/` | Production-ready (SKILL.md v2.3, 8KB + references/methodology-socratic-dialog.md) |
| `prompts/` | Empty (README only) | — | `prompts/` | Empty |
| `commands/` | Empty (README only) | — | `commands/` | Empty |
| `integrations/` | Empty (README only) | — | `integrations/` | Empty |

**Net:** 3 publication-ready assets, **all under MIT**. `prompts/`, `commands/`, `integrations/` are scaffolded but empty — not part of Sprint 0.

> **License decision (recorded 2026-06-18):** All three assets unified under **MIT**. `socratic-dialog` was re-licensed by the sole author (Monika Zapisek) from CC-BY-4.0 to MIT. Earlier copies distributed under CC-BY-4.0 retain that license for prior recipients; new copies and derivative work are MIT.

---

## 2. Channels (the landscape)

| Channel | Format | Reach | Effort | License fit | Priority |
|---|---|---|---|---|---|
| **GitHub** (already public — design-engineering-playbook repo) | README + repo structure | Existing audience, organic SEO | Already done | MIT | P0 (foundation) |
| **Awesome Copilot** (github/awesome-copilot) | Folder of `*.md` files in `agents/` or `skills/` subdirectory + frontmatter | ~17k installs via dedicated vsce extension, official Microsoft-backed curation | Low–Medium (format adapt + PR) | MIT (all 3 assets) | P0 (highest ROI) |
| **VS Code Agent Plugins (Preview)** | `plugin.json` + `agents/` + `skills/` | New, growing, cross-tool (VS Code + Copilot CLI + Claude Code) | High — API still moving, format not stable | MIT (all assets, single license) | P2 (wait for stable API) |
| **Cursor** | `.cursorrules` + custom prompts/rules | Fast-growing, dev-tool audience | Medium — need to test format | MIT | P1 (dev audience overlap) |
| **skills.sh** (npx skills add) | Public GitHub repo with SKILL.md files — already installable | Growing, cross-agent (Claude Code, Copilot, Cursor, Codex) | Zero — repo is already public and compatible | MIT | P0 (already live) |
| **Medium** | Long-form articles — **SoT for all written content** | 100M monthly readers, Twoja audience tam czyta | Medium — content production | MIT | P1 (primary writing channel, SoT) |
| **X.com** | Thread + link do Medium artykułu | Discovery, networking, PD + AI community | Low — thread per artykuł | MIT | P1 (distribution, not SoT) |
| **Personal site** (monikazapisek.com) | Thumbnail + tytuł + link do Medium (nie pełny artykuł) | Portfolio, landing, SEO | Low — thumbnail only, nie duplikuj treści | MIT | P1 (showcase, not SoT) |
| **dev.to** | Opcjonalny cross-post | Developer audience, słabe dopasowanie do PD | Low | MIT | P3 (nie Twoja audience) |
| **Substack** | Newsletter z własną listą | Owned audience | Medium — wymaga regularnego rytmu | MIT | P3 (odkładamy) |
| **YouTube** | Wideo walkthroughs | Duży reach, Twoja audience tam jest | High — zupełnie inny format | MIT | P2 (osobna decyzja) |
| **Prompt marketplaces** (PromptHero, FlowGPT, etc.) | Standalone prompts | Słaby signal, brak attribution | High | Mixed | P3 (low ROI) |

**Content flow (decided 2026-06-18):** Medium (write + publish, SoT) → X.com (thread + link) → Personal site (thumbnail + link, no duplicate).

**Excluded from roadmap:** paid marketplaces without strong attribution discipline; LinkedIn carousel mills; Anthropic Claude Marketplace (enterprise-only); Figma Community (wrong format); dev.to (not Twoja audience).

---

## 3. Kano model applied to the channels

For each channel, classify what the user (you + your audience) gets:

| Channel feature | Kano category | Why |
|---|---|---|
| Asset has clean frontmatter (name + description + license) | **Must-be** | Without it, submission is auto-rejected |
| License clearly stated in README | **Must-be** | GitHub, awesome-copilot both require |
| Works as standalone (no hidden private deps) | **Must-be** | Public users can't reach your `.agents/` |
| Asset works in both Claude Code and Copilot format | **Performance** | More reach = more value, but each format is incremental |
| Published under your name (Monika Zapisek / Design Engineering Playbook) | **Performance** | Brand value, but anonymous PR also works |
| Cross-channel link (e.g., awesome-copilot entry points to your repo) | **Attractive** | Earns 7-day love from discovery users |
| Video walkthrough / demo per asset | **Attractive** | High cost, high reward — defer unless research confirms demand |
| Multi-language README (PL + EN) | **Indifferent** for now | Your audience is bilingual but reads English technical content by default; cut until asked |
| Chatbot-style Q&A promo on social | **Reverse** | Audience reads your work, doesn't want "AI hype" posts; cut |

**MDP pick:** cross-channel link — costs ~1 hour to add, doubles the discoverability of every asset.
**Kills:** multi-language README, chatbot promo posts — free up ~2 days of writing capacity for actual asset polish.
**Must-be hardening:** frontmatter + license + standalone-test gates become a single CI check before any PR.

---

## 4. Strategy (the choice architecture)

### 4.1 Positioning

**Dual brand:**
- **Author (every frontmatter, README byline):** Monika Zapisek
- **Project (README hero, repo header):** Design Engineering Playbook
- **Rule of thumb:** byline = person, container = project

**Tagline (one sentence):**
> "AI-assisted workflow artefacts for product designers working in agile and lean environments."

### 4.2 Format unification

All 3 publication-ready assets must satisfy this contract before any submission:

```yaml
# Required frontmatter for awesome-copilot / VS Code / Cursor compatibility
---
name: <kebab-case-name>
description: |
  <2-4 sentences: what it does, when to use, when NOT to use>
license: MIT
model: Claude Sonnet 4.5
compatibility: |
  Tested with Claude Sonnet 4.5 (Claude Code), GPT-5.5, MiniMax-m3, GitHub Copilot.
  Designed for Claude Code, Codex, VS Code, OpenCode.
  No external dependencies, no MCP required.
metadata:
  author: Monika Zapisek
  version: <x.y>
  project: Design Engineering Playbook
---
```

**Model + compatibility policy (decided 2026-06-18):**

- **`model:` is always a single string** — `Claude Sonnet 4.5`. awesome-copilot frontmatter schema does not support multi-model lists; do not invent a `model-alternatives` field.
- **`compatibility:` distinguishes facts from intent** — `Tested with:` lists only models the author has actually run (Claude Sonnet 4.5, GPT-5.5, MiniMax-m3, GitHub Copilot as of 2026-06-18 smoke test); `Designed for:` lists target platforms that are planned for validation in subsequent sprints (Claude Code, Codex, VS Code, OpenCode, plus Claude.ai + Messages API for API-first skills like `socratic-dialog`).
- **Do NOT list unavailable Copilot models** (e.g. `MiniMax-m3` is a valid tested-with claim for the Mavis runtime, but is **not** in the GitHub Copilot model picker — never advertise it as a Copilot model).
- **`GitHub Copilot` is a tested-with claim as of 2026-06-18** — Copilot smoke test (`integrations/copilot-smoke-test.md`) passed for all 3 assets after the GitHub Copilot refactor. The `Designed for:` entry for Copilot was removed from frontmatter in all 3 assets; any future re-introduction must be re-validated.

### 4.3 Submission order (sequenced for momentum)

1. **GitHub** — already public. **No work.**
2. **Awesome Copilot PR #1** — `agent-agile-master` (highest visibility, demonstrates seriousness)
3. **Awesome Copilot PR #2** — `kano-model-strategist` skill (smaller, faster PR, builds reviewer trust)
4. **Awesome Copilot PR #3** — `socratic-dialog` (after import to `skills/`; license is MIT, attribution note in §1 of this doc explains the relicense)
5. **Cursor** — package the same 3 assets as `.cursorrules` rules or workspace snippets
6. **Personal site post** — "Three agents I shipped this quarter" with links back to all of the above
7. **VS Code Agent Plugins** — wait until plugin.json spec stabilizes (preview churn)

**Rationale:** awesome-copilot is the bottleneck because (a) it's a PR review by maintainers, not auto-publish, so first impressions matter; (b) shipping the strongest asset first (full agent) sets quality bar; (c) smaller PRs after a successful one get faster reviews.

### 4.4 Attribution discipline

- Every published asset must list author = Monika Zapisek and project = Design Engineering Playbook in frontmatter
- Every PR description must link to canonical repo + SYNCHRONIZATION.md (if applicable)
- Every README that cites a third-party framework must include ATTRIBUTION.md
- License clarity is a hard gate — no PR goes out without explicit license field

---

## 5. Roadmap

### Sprint 0 — Strategy & Inventory (this document)
**Status:** complete.
**Outputs:** this file.
**Time spent:** ~1 hour.

### Sprint 1 — Minimum Viable Distribution (2 days, **the path I'd take**)
**Goal:** Get 1 asset into 1 channel with a clean submission that won't embarrass us.

**Day 1:**
- [x] Decide license for `kano-model-strategist` (MIT, 2026-06-18)
- [x] Import `socratic-dialog` into `skills/` (Copy-Item, relicensed CC-BY-4.0 → MIT, 2026-06-18)
- [x] Add required frontmatter (`model`, `compatibility`, `metadata.author`) to all 3 assets (2026-06-18)
- [x] Add LICENSE field decision to README of each asset (LICENSE files updated, AGENT.md/SKILL.md frontmatter complete)

**Day 2:**
- [ ] Format `agent-agile-master` for awesome-copilot submission (folder copy, README adapted, license confirmed)
- [ ] Open Draft PR against `github/awesome-copilot`
- [ ] Self-review with awesome-copilot's CONTRIBUTING.md checklist

**Definition of done:** PR is open (not merged), passes automated checks, has clear title + body linking to canonical repo.

### Sprint 2 — Full Launch (2 weeks, **the path if Sprint 1 lands well**)
**Week 1:**
- Day 1–2: Merge Sprint 1 PR if not yet (or address review feedback)
- Day 3:   Submit `kano-model-strategist` as separate PR
- Day 4:   Submit `socratic-dialog` as separate PR (license MIT; PR body links to the relicense note in `playbook/distribution/strategy-and-roadmap.md` §1)
- Day 5:   Add cross-channel links in awesome-copilot PRs (each → canonical repo)

**Week 2:**
- Day 1–2: Cursor submission — package 3 assets as `.cursorrules` + project rules
- Day 3:   Personal site post draft
- Day 4:   Publish site post + cross-link to all 3 channels
- Day 5:   Measure: GitHub stars, awesome-copilot install count, Cursor rule installs, site traffic

### Sprint 3 — Stabilization (backlog)
- VS Code Agent Plugin submission (when plugin.json spec stabilizes)
- Update awesome-copilot entries with first user feedback
- Quarterly: audit license + frontmatter across all assets
- Backlog: `prompts/`, `commands/`, `integrations/` — only fill if user demand signal appears

---

## 6. Risks & mitigations

| Risk | Probability | Impact | Mitigation |
|---|---|---|---|
| awesome-copilot maintainers reject format | Medium | Medium | Read CONTRIBUTING.md twice; mirror 2 existing successful submissions exactly |
| License mismatch blocks PR | Low | High | License decision is Day 1 of Sprint 1, not Day 2 |
| `socratic-dialog` import breaks existing references | Low | Medium | Copy-Item, don't Move; verify SKILL.md loads in both Claude Code and Copilot |
| Brand confusion (Monika vs Design Engineering Playbook) | Medium | Low | Single rule: byline = person, container = project. Document once, apply everywhere |
| VS Code Agent Plugin API changes mid-Sprint | High | Low | Defer to Sprint 3; not on critical path |
| ~~`Designed for: GitHub Copilot` claim without refactor validation~~ (added 2026-06-18, **closed 2026-06-18**) | ~~Medium~~ | ~~High~~ | **Closed:** Copilot refactor + smoke test passed 2026-06-18. GitHub Copilot now in `Tested with:` for all 3 assets (commit `0d2953e feat(integrations): add Copilot support and smoke test results`). Evidence: `integrations/copilot-smoke-test.md`. |

---

## 7. Open questions (decide before Sprint 1 Day 1)

**Status: §7 closed 2026-06-18 (Sprint 1 Day 1 executed).**

| # | Question | Decision | Date |
|---|---|---|---|
| 1 | License for `kano-model-strategist` | **MIT** (matches agent + socratic-dialog after relicense) | 2026-06-18 |
| 2 | `socratic-dialog` license | **MIT** (relicensed from CC-BY-4.0 by sole author; prior recipients retain CC-BY-4.0 for their copies) | 2026-06-18 |
| 3 | Model in frontmatter | **Claude Sonnet 4.5** (single string, awesome-copilot schema) | 2026-06-18 |
| 4 | `compatibility:` claim scope | **Tested with** Claude Sonnet 4.5 (Claude Code), GPT-5.5, MiniMax-m3, **GitHub Copilot** (smoke test passed 2026-06-18). **Designed for** Claude Code, Codex, VS Code, OpenCode; `socratic-dialog` additionally Designed for **Claude.ai** + **Messages API** (API-first skill, no runtime required). | 2026-06-18 |

**Remaining Sprint 1 Day 2 questions (defer, do not block Day 1):**

5. **Cursor submission format** — `.cursorrules` file or project rules UI? *Recommendation: both — `.cursorrules` is the installable artifact, UI rules are user-curated.*
6. **Personal site platform** — is `monikazapisekstudio/meta-space` the canonical blog, or just a repo? *Recommendation: confirm before writing the Sprint 2 site post.*
7. **awesome-copilot category placement** — `agents/` (full agent) or `skills/` (kano, socratic)? *Recommendation: agent goes in `agents/`, both skills go in `skills/`, with cross-links.*

---

## 8. Definition of done (overall strategy)

- 3 assets publicly reachable from at least 2 channels (GitHub + awesome-copilot minimum)
- All assets pass the frontmatter contract (§4.2)
- All assets have clear license + author + project attribution
- At least one PR successfully merged to awesome-copilot
- Personal site post published with cross-links
- Quarterly review cadence established

---

## 9. Next action

Sprint 1, Day 1. Pick from §7 open questions — especially the license decision, which blocks all other work.