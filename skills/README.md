# Skills

Skills are reusable AI workflows.

Use them to turn repeated design engineering work into procedures an AI assistant can follow consistently.

A skill is not a random prompt. It is a defined workflow for repeated execution of a checklist, review process, method, or multi-step task.

Detailed authoring rules live in `skills-guideline.md`.

## Available Skills

* **[socratic-dialog](./socratic-dialog/)** — Enforces reasoning rigor, anti-fluency, and anti-sycophancy guards on the agent. Operates as a Cognitive Immune System for reasoning: three lines of defense (Definition, Elenchus, Faithfulness) protect the reasoning chain from unsupported claims, with an autoimmunology checkpoint preventing self-attack on verified conclusions. Use in Context Engineering for Story Map verification, strategic planning, and requirements gathering.
* **[kano-model-strategist](./kano-model-strategist/)** — Classifies features into Kano categories (Must-be / Performance / Attractive / Indifferent / Reverse / Questionable) and prunes the backlog to prevent Experience Rot. Forces a "Start with NO" stance on new features. Includes T-shirt sizing rubric, CEO pushback scripts, and a market-access vs. user-facing feature distinction. Use for product backlog triage, MVP/MDP scoping, or any "should we build this" decision.

Each skill lives in its own folder. See the skill's `SKILL.md` for the full description, workflow, and usage. Per-skill licensing is documented in each skill's `LICENSE` file (if present).
