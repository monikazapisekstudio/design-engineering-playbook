---
created: 2026-07-20
updated: 2026-07-20
version: 1.1
description: Canonical specification for the LLM-ready FigJam Story Map template (Patton methodology). Built and validated on a real design-system Story Map board.
---

# FigJam Story Map Template — LLM-ready (Patton methodology)

FigJam canvas template compliant with Jeff Patton's User Story Mapping methodology, optimised for error-free reading by LLMs (REST API JSON + Vision). Built and tested on a real design-system Story Map board.

## Canvas structure

```
[STORY_MAP]                                    ← root SECTION (wrapper, required)
├── [00_SECTION_AI_Readme]                     ← system prompt + legend
├── [TEMPLATE_META]                             ← attribution block (author, version, license, repo)
├── [USER_SEGMENT_or_PERSONA]                  ← persona + Name + Description (optional image)
├── [01_SECTION_BACKBONE_Activities]            ← backbone L1
│   └── [ACT_01] Activity  ·  [ACT_02] Activity
├── [02_SECTION_BACKBONE_User_Tasks]           ← backbone L2
│   └── [TASK_01] Task  ·  [TASK_02] Task  ·  [TASK_03] Task
├── [03_SECTION_Release_1] Core Value Proof     ← V1 with full taxonomy
├── [04_SECTION_Release_2] Business Goal ...    ← V2 clean
└── [05_SECTION_Release_3] Business Goal ...    ← V3 clean
```

## Template Metadata — attribution block `[TEMPLATE_META]`

Insert as a separate Section between `[00_SECTION_AI_Readme]` and `[USER_SEGMENT_or_PERSONA]`. The parser ignores it (it reads only STICKY / SHAPE_WITH_TEXT / CONNECTOR with `[STORY]` / `[ACT]` / `[TASK]` tags — this block is plain text). Clean separation of concerns: agent instructions in `[00]`, human attribution in `[TEMPLATE_META]`, map content in the remaining sections.

### Canonical `[TEMPLATE_META]` content

```text
Author: Monika Zapisek
Website: monikazapisek.com
Created: 2026-07-20
Last Updated: 2026-07-20
Version: 1.0
Licence: MIT
Skill: github.com/monikazapisekstudio/design-engineering-playbook/tree/main/skills/figjam-storymap-llm
Get the skill (free, MIT): https://clawhub.ai/monikazapisekstudio/skills/figjam-storymap-llm

If you use this template, credit appreciated:
"Based on figjam-storymap-llm by Monika Zapisek"

FigJam and Figma are trademarks of Figma, Inc. This template is
independent and not affiliated with, endorsed by, or sponsored by Figma, Inc.
```

### What `[TEMPLATE_META]` must contain

| Field | Value | Why |
|---|---|---|
| Author | Full name | Build-in-public credit, social proof — anyone who duplicates the template sees the author |
| Website | Author URL | Profile visits → followers |
| Created | ISO 8601 date (`YYYY-MM-DD`) | When the template was created — tracking which version is in use |
| Last Updated | ISO 8601 date (`YYYY-MM-DD`) | Bump on every change — users know whether they have the fresh version |
| Version | semver (`1.0`, `1.1`, `2.0`) | Template versioning — important when the template is forked / duplicated |
| Licence | `MIT` (or other) | Explicit licence statement — users know whether they can duplicate / modify / sell |
| Skill (GitHub) | full URL to the skill folder in the repo | Opens the folder landing page (rendered README) — routes to parser, full procedure, source code |
| Skill (ClawHub) | `https://clawhub.ai/monikazapisekstudio/skills/figjam-storymap-llm` | ClawHub is a skills marketplace — one-click install for Claude Code / Cursor / Copilot. Prefer this link in templates (install path), GitHub as source-of-truth in skill repos |
| Credit appreciated | soft request for citation | Ethical ask (MIT does not require it), builds the authority loop — every screenshot of the template = free advertising |
| Trademark disclaimer | FigJam/Figma = Figma, Inc. | Defense-in-depth — nominative fair use is legal, disclaimer is a safety net |

### What NOT to put in `[TEMPLATE_META]`

- ❌ Full MIT licence text (21 lines — a repo link is enough)
- ❌ Contact email (spam risk — you have a Website)
- ❌ `© 2026 Monika Zapisek` — MIT LICENSE already contains it, do not duplicate
- ❌ "All rights reserved" — MIT is permissive, "all rights reserved" contradicts the licence
- ❌ Long skill description — that lives in the repo README, not on the canvas
- ❌ Follow / X handle — optional, only if you have an active account and want to build an audience

## Colour palette (semantic + deterministic for Vision LLM)

| Section / element | HEX | Meaning |
|---|---|---|
| `[ACT_*]` Activity | `#FFD9E2` / `rgba(255, 217, 226, 0.77)` | Backbone L1 — main user goal |
| `[TASK_*]` Task | `#FFE5D2` | Backbone L2 — step in the procedure |
| `[STORY] [V1]` | `#E6F6C3` (light green) | Release 1 — MVP / Core Value |
| `[STORY] [V2]` | `#E5F3FE` (light blue) | Release 2 — Growth |
| `[STORY] [V3]` | `#F3EEFF` (light purple) | Release 3 — Scale / Vision |
| Persona (sticky) | `#B3EFBD`, `#B3F4EF`, `#FFD3A8`, `#D3BDFF` | 4 segments: Designer / Developer / End-user / AI-agent |
| Connectors (default) | `#D5C2C5` | Causal relations |
| Connectors (block) | red | Blockers (A BLOCKS B) |

## Typography

- **Title (Story Map):** Inter Bold 96px
- **Section header (Activity / Task / Release):** Inter Bold 96px, section colour
- **Description text:** Inter Medium 40px, section colour
- **Sticky text:** Inter Medium 16px

## Sticky tag taxonomy

### Story (V1 — full)

```text
[STORY] [V1] [P1] User Story sentence @DEV
Acceptance Criteria:
- Acceptance criterion 1
- Acceptance criterion 2
```

### Story (V2 / V3 — clean)

```text
[STORY] [V2] User Story sentence
Acceptance Criteria:
- Acceptance criterion 1
```

**Zero `[P*]`, zero `@Owner` in V2/V3** (Lean UX — planning distant hypotheses is Big Upfront Design).

### Activity (backbone L1)

```text
[ACT_01] Activity
```

### Task (backbone L2)

```text
[TASK_01] Task
```

## Layout (X and Y axes)

- **X axis (chronology):** left → right. `[ACT_01]` → `[ACT_02]`, within an activity `[TASK_01]` → `[TASK_02]` → `[TASK_03]`. Each task is its own column.
- **Y axis (priority / release):** top → bottom. Backbone at the top (Activities, then Tasks), release slices below (V1, V2, V3).
- **Story in a release:** a `[STORY]` sticky stacks vertically under the task it belongs to (parser algorithm: `center_x` of the story must fall within the task's X range).
- **Column spacing:** 40–60 px horizontally — gives the algorithm a large error margin.
- **Do not overlap columns:** as long as a sticky from one column does not slide more than halfway under the neighbouring task, the parser will not misfire.

## Connectors

### When to use

- **Branching (alternative flows):** `[STORY_05] --[IF_FAIL]--> [STORY_05B] Error screen`
- **Cross-release dependencies:** `[STORY_12_V2] --[REQUIRES]--> [STORY_03_V1]`
- **Acceptance criteria / notes:** a clarifying sticky attached to the main story (though AC inline in the same sticky is preferred)

### When NOT to use

- **Linear chronological flow** (step 1 → step 2 → step 3). Chronology is encoded in X position + `[TASK_*]` numbering. 100 arrows = spaghetti payload.

## `[00_SECTION_AI_Readme]` — agent instruction

Insert at the start of the canvas (ideally `x: 0, y: 0` relative to the root). This is the agent's brain on the canvas — without it the agent guesses, with it the agent acts deterministically. Insert as **a single TEXT node** (do not split into separate stickies — the agent reads this as one instruction document).

```text
==================================================
SYSTEM INSTRUCTIONS FOR AI AGENT (FIGJAM PARSER)
==================================================
PURPOSE:
This file contains a Story Map (Jeff Patton methodology) for the product
[PRODUCT NAME]. Parse it as a living specification, not as a screenshot.

SKILL:
This FigJam template is part of the figjam-storymap-llm skill by Monika Zapisek.
The skill audits and parses FigJam User Story Maps into LLM-readable
Markdown / JSON — eliminates the post-workshop transcription step and feeds
Story Maps to coding agents (Cursor, Claude Code, Copilot) as living spec.
What you get:
- Python parser (Figma REST API -> Markdown / JSON)
- Canonical FigJam template spec (this file's structure)
- Verification prompt for LLM-readiness audits
- Map Structure Guardian (active coach for Patton + Cohn INVEST rules)
- Lean UX rules baked in (V1 tagged, V2 / V3 clean)
Get the skill (free, MIT licence):
https://clawhub.ai/monikazapisekstudio/skills/figjam-storymap-llm
Install:
- Claude Code / Cursor / Copilot: load the SKILL.md from the link above
- CLI parser: clone the repo, run scripts/figjam_parser.py --file-key {KEY} --token $FIGMA_TOKEN
- Audit mode: paste references/system-prompt.md as System Instructions, share board screenshot

CANVAS STRUCTURE:
- Root: [STORY_MAP] — all stickies must be inside (otherwise unsectioned_nodes in JSON)
- Sections vertical (Y axis): [TEMPLATE_META] -> [USER_SEGMENT_or_PERSONA] ->
  [01_BACKBONE_Activities] -> [02_BACKBONE_User_Tasks] ->
  [03_Release_1] -> [04_Release_2] -> [05_Release_3]
- Chronology encoded in X axis (Task 01 -> Task 02 -> Task 03)
- Each [STORY] mapped to [TASK] algorithmically: center_x of story falls
  into the X range of the task (task.x to task.x + task.width)

COLOR SEMANTICS:
- #FFD9E2 = Activity (backbone L1, main user goal)
- #FFE5D2 = Task (backbone L2, discrete user action, Patton term — NOT "Step")
- #E6F6C3 = Story V1 (MVP, with [P*] and @Owner)
- #E5F3FE = Story V2 (Growth, clean)
- #F3EEFF = Story V3 (Scale / Vision, clean)

TAXONOMY:
Canonical sticky syntax:
[STORY] [V1] [P1] User Story sentence @DEV
Acceptance Criteria:
- Acceptance criterion 1
- Acceptance criterion 2

TAGS:
[STORY] = User Story (release slice)
[V1] / [V2] / [V3] = Release identifier
[P1] / [P2] / [P3] = Priority — V1 ONLY
@UX / @DEV / @PM / @QA = Owner role — V1 ONLY
[ACT_*] = User Activity (backbone L1)
[TASK_*] = User Task (backbone L2 — Patton term, NOT "Step")

LEAN UX RULES (HARD):
- V1 (MVP): full taxonomy — [P1]/[P2]/[P3] + @Owner + AC inline
- V2 / V3: clean — zero [P*], zero @Owner
- Reason: planning distant hypotheses is Big Upfront Design (Patton + Gothelf)
- Exception: none — if you find [P*] or @Owner in V2/V3, FLAG as anti-pattern

CONNECTOR RULES:
- Arrow A -> B = causal relation (A causes B)
- Red edge = block (A BLOCKS B)
- Edge label = relation type (REQUIRES, IF_FAIL, BLOCKS)
- DO NOT connect linearly (step 1 -> step 2 -> step 3) — chronology is in X + [TASK_*] numbering
- Use native Connectors only (they have connectorStart / connectorEnd in JSON)
- Pen-tool lines = ignore (vectors without relation semantics)

AC RULES (HARD):
- AC lives in the same sticky as [STORY], after the "Acceptance Criteria:" marker
- Separate AC sticky = anti-pattern (two disconnected JSON objects, agent guesses by x,y)
- If you see a separate AC sticky, FLAG and propose merge with nearest Story

PARSING METHODS (best to worst):

1. GOLD STANDARD — Figma REST API (JSON)
   URL: https://www.figma.com/developers/api
   Endpoint: GET /v1/files/{file_key}
   Auth: header X-Figma-Token
   How it works: fetches full node tree (SECTION, STICKY, SHAPE_WITH_TEXT, CONNECTOR)
   Pros: 100% deterministic, zero OCR, zero hallucinations, full metadata (x, y, section, connectorStart/End)
   Cons: requires a valid FIGMA_TOKEN (Figma personal access token from settings)
   Use when: production, large boards (>50 stickies), repeated parsing

2. FALLBACK — PNG / screenshot (Vision LLM)
   How it works: FigJam screenshot -> Claude 3.5 Sonnet / GPT-4o (Vision mode)
   Pros: quick, no API token needed
   Cons:
   - OCR errors on >100 stickies (small text)
   - Section names may be clipped by Copy as PNG (label renders on outer frame edge)
   - No spatial metadata (x, y) — agent loses story->task mapping
   - Dense layouts confuse the agent
   Defense: add internal text headers inside each section (do not rely only on frame label)
   Use when: quick audit, small boards (<50 stickies), no API token

3. NOT RECOMMENDED — PDF export
   Why NOT:
   - PDF export converts text to vectors / text streams
   - Spatial dependency extraction (x, y) most error-prone
   - Section hierarchy often lost (PDF does not preserve FigJam hierarchy)
   - Connectors become lines without relation semantics
   Do not use. If you only have PDF, route through Figma REST API (JSON) instead.

OUTPUT EXPECTED:
Markdown backlog ordered: Release -> Activity -> Task -> User Stories (with AC + Owner)

FLAG (active coach — do not silently fix, report with node IDs and smallest concrete fix):
- Build-first voice in [ACT_*] / [TASK_*] ("Build X" instead of "User does X") — Patton anti-pattern
- V2 / V3 with [P*] or @Owner — Big Upfront Design
- Separate AC sticky — gets lost in JSON
- Stickies outside [STORY_MAP] root — unsectioned_nodes, parser will not find them
- Connector cycles within the same release — suspected duplicate Story or missing dependency
- Connectors for linear flow — spaghetti payload, chronology is in X + [TASK_*] numbering
==================================================
```

**Tip:** In the block above, replace `[PRODUCT NAME]` with the actual product name before publishing the template.

## Pre-publish checklist (10 min)

Before publishing the template as an "LLM-ready FigJam Story Map", verify:

- [ ] **Root `[STORY_MAP]`** wraps the entire canvas (zero `unsectioned_nodes` in JSON)
- [ ] **`[00_SECTION_AI_Readme]`** exists and contains legend + connector rules + expected output
- [ ] **`[TEMPLATE_META]`** exists between `[00]` and `[USER_SEGMENT]` — contains Author, Created, Last Updated, Version, Licence, Skill URL, credit appreciated, trademark disclaimer
- [ ] **`[01_SECTION_BACKBONE_Activities]`** contains only `[ACT_*]`
- [ ] **`[02_SECTION_BACKBONE_User_Tasks]`** contains only `[TASK_*]`, columns have 40–60 px spacing
- [ ] **`[03_SECTION_Release_1] Core Value Proof`** — `[STORY] [V1]` stickies with `[P1]/[P2]/[P3]`, `@Owner`, AC inline
- [ ] **`[04_SECTION_Release_2]`** and **`[05_SECTION_Release_3]`** — `[STORY] [V2]/[V3]` stickies clean (zero `[P*]`, zero `@Owner`)
- [ ] **AC inline** — in the same sticky as `[STORY]`, after `Acceptance Criteria:`
- [ ] **Connectors** only for branching / cross-release dependencies
- [ ] **Internal text headers** in each section (defense against `Copy as PNG` clipping section labels)
- [ ] **No FigJam Stamps / Badges** as information carriers (use text prefixes inside the sticky instead)
- [ ] **`Last Updated`** in `[TEMPLATE_META]` refreshed before publishing (today's ISO 8601 date)

## Parser test (after filling the template)

```bash
python scripts/figjam_parser.py --file-key {FILE_KEY} --token $FIGMA_TOKEN > story-map.md
```

Verify:

- Each `[STORY]` has an assigned `[TASK]` (or is flagged `UNASSIGNED`)
- AC stays in the same section as the story
- V2 / V3 are clean
- Connectors render as `A --[label]--> B`

## Pattoian notes (Patton + Lean UX)

- **Release naming:** `Core Value Proof`, `Business Goal or Outcome` — outcome, not "v2 for v2". Patton encourages giving a short business goal next to the version number.
- **Priorities only in V1:** position on the Y axis within V1 + `[P1]/[P2]/[P3]` inside the release. V2 / V3 are hypotheses.
- **Owner only in V1:** assigning owners to distant features is noise.
- **Story Map = user perspective, not builder perspective.** Activities / Steps describe what the **user** does ("Buy Component Package", "Check External Documentation"), not what the team builds ("Build X", "Create Y").
- **Term "Task" (not "Step").** Patton standard for backbone L2.