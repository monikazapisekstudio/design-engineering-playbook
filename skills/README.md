# Skills

Skills are reusable AI workflows.

Use them to turn repeated design engineering work into procedures an AI assistant can follow consistently.

A skill is not a random prompt. It is a defined workflow for repeated execution of a checklist, review process, method, or multi-step task.

Detailed authoring rules live in `skills-guideline.md`.

## Available Skills

* **[legible-agent-output](./legible-agent-output/)** — Force every user-facing string from an AI agent to be readable by a non-technical human without external context. Replaces opaque codes (A127, ENOENT), framework jargon (`cycle 2 dispatch`, `Phase 2: post-merge validation`), raw error strings, and bare percentages with plain-language titles, status messages, and error descriptions. 7 laws, 6-category failure-mode taxonomy, 30+ worked before/after transformations, 3-prompt eval loop. Use when an agent emits task titles, status messages, error messages, action previews, plan summaries, cycle reports, or sub-agent delegation prompts.
* **[socratic-dialogue](./socratic-dialogue/)** — Enforces reasoning rigor, anti-fluency, and anti-sycophancy guards on the agent. Operates as a Cognitive Immune System for reasoning: three lines of defense (Definition, Elenchus, Faithfulness) protect the reasoning chain from unsupported claims, with an autoimmunology checkpoint preventing self-attack on verified conclusions. Use in Context Engineering for Story Map verification, strategic planning, and requirements gathering.
* **[kano-model-strategist](./kano-model-strategist/)** — Classifies features into Kano categories (Must-be / Performance / Attractive / Indifferent / Reverse / Questionable) and prunes the backlog to prevent Experience Rot. Forces a "Start with NO" stance on new features. Includes T-shirt sizing rubric, CEO pushback scripts, and a market-access vs. user-facing feature distinction. Use for product backlog triage, MVP/MDP scoping, or any "should we build this" decision.

Each skill lives in its own folder. See the skill's `SKILL.md` for the full description, workflow, and usage. Per-skill licensing is documented in each skill's `LICENSE` file (if present).
