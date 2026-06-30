# Awesome Copilot — Submission Workspace

**Purpose:** Pre-formatted, self-reviewed assets ready for PR submission to
[`github/awesome-copilot`](https://github.com/github/awesome-copilot).

**Status:** Sprint 1 Day 2 (P0 — `agent-agile-master` formatted; P1 skills pending).

---

## Files in this folder

| File | Submission order (§4.3 of strategy-and-roadmap) | Status |
|---|---|---|
| `agent-agile-master.agent.md` | **PR #1** (highest visibility, demonstrates seriousness) | 🟢 Self-reviewed, ready to open Draft PR |
| `kano-model-strategist.skill.md` | PR #2 (smaller, builds reviewer trust) | 🔴 Not yet formatted |
| `socratic-dialogue.skill.md` | PR #3 (after Sprint 2 Day 4 — relicense attribution note required) | 🔴 Not yet formatted |

---

## Submission process (per awesome-copilot CONTRIBUTING.md)

1. **Fork** `github/awesome-copilot`.
2. **Branch from `staged`** (NOT `main` — see CONTRIBUTING "Submitting Your Contribution" section).
3. **Copy** the formatted file from this folder to the appropriate location in the fork:
   - Agents → `agents/<filename>.agent.md` in the fork.
   - Skills → `skills/<skill-name>/SKILL.md` in the fork (folder structure required).
4. **Run** `npm install && npm start` in the fork to update README tables.
   - If the README would change, the PR check will fail — re-run until clean.
5. **Open Draft PR** targeting the **`staged`** branch in `github/awesome-copilot`.
6. **PR title suffix:** `🤖🤖🤖` if submitting as an AI agent (fast-track per CONTRIBUTING).
7. **Wait for review** — typical turnaround is a few days; may require maintainer nudge.

> ⚠️ **Critical:** Do **NOT** target `main` in the PR. CONTRIBUTING explicitly warns that
> branches from `main` "will cause merge conflicts and delays in processing your contribution,
> or they may be outright rejected."

---

## Pre-submission checklist (per `playbook/quality-requirements.md` Quality Gates)

Before opening a PR, confirm every box:

- [ ] Frontmatter contract (`strategy-and-roadmap.md` §4.2) — `name`, `description`, `license`,
      `model`, `compatibility: Tested with / Designed for`, `metadata: author / project / version`
- [ ] Smoke test evidence in `integrations/copilot-smoke-test.md` for every claimed runtime
- [ ] `DOD-CHECKLIST.md` (per-asset) fully ticked
- [ ] Version bump in frontmatter matches `CHANGELOG.md` entry
- [ ] Root `README.md` index reflects the asset (auto-checked by awesome-copilot `npm start`)
- [ ] License + author + project attribution present in frontmatter AND PR body
- [ ] Self-review against `CONTRIBUTING.md` completed (filename, location, sections present)

---

## Why this folder structure

We keep the formatted asset in `integrations/awesome-copilot/` (this folder) rather than
mirroring it directly into `agents/agent-agile-master/dist/` because:

1. **Single source of truth** — `agents/agent-agile-master/AGENT.md` is canonical; this folder
   is the *adapted* preview for one specific channel.
2. **Multi-channel reuse** — when we later format for Cursor (`.cursorrules`) or VS Code Agent
   Plugins (`plugin.json`), each lives in its own integrations subfolder with the same shape.
3. **Easy PR diff** — reviewers in our own repo can see exactly what changes when adapting
   to a new channel, without spelunking through `dist/` subfolders.

---

## Per-file submission instructions

### `agent-agile-master.agent.md` → PR #1

**Target branch in fork:** `staged`
**File destination in fork:** `agents/agent-agile-master.agent.md`
**PR title:** `feat(agents): add agent-agile-master solo practitioner ritual orchestrator 🤖🤖🤖`
**PR body:** See `pr-body-agent-agile-master.md` (in this folder) for the full template.

**Why this asset first:**
- Highest visibility (full agent, not a single skill)
- Demonstrates seriousness — v1.3, public source, MIT, full attribution
- Builds reviewer trust for the two smaller skill PRs that follow
- Reuses our `playbook/distribution/strategy-and-roadmap.md` §4.3 submission order

### `kano-model-strategist.skill.md` → PR #2

🔴 Pending — schedule for Sprint 1 Day 2 after PR #1 is opened (parallel work OK, but
submit PR #1 first so reviewer can give feedback on style before we batch).

### `socratic-dialogue.skill.md` → PR #3

🔴 Pending — schedule for Sprint 2 Day 4. Requires additional attribution note in PR body
explaining the CC-BY-4.0 → MIT relicense by the sole author (see §1 of strategy-and-roadmap).