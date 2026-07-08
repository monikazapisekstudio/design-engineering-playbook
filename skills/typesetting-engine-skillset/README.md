# Typesetting Engine Skillset

**Six single-responsibility skills covering the full typography/layout pipeline — from character-level polish to Figma-native design tokens.**

Each skill does one job and hands off to its neighbors rather than duplicating logic. Use one in isolation, or run the relevant subset in sequence for a full pass on a design or a piece of body copy.

## The six skills

| Skill | Scope | Design-tool aware |
|---|---|---|
| [`microtypography`](./microtypography/) | Character-level text polish: hanging single-letter conjunctions, numbers/units, smart dashes/quotes, widows/orphans, ragged edges, hanging punctuation (detection). Format-agnostic — markdown, HTML, plain text. | Flags Figma-specific cases, hands off computation to `text-typesetting` |
| [`line-length-optimizer`](./line-length-optimizer/) | Column width (measure): 45–75 characters desktop, 35–45 mobile. Outputs a `ch`-based CSS fix or resizes a Figma text node. | Yes — reads `textAutoResize` |
| [`text-typesetting`](./text-typesetting/) | Line-height, letter-spacing/tracking (case-, x-height-, weight-, variable-axis-aware), vertical-trim, OpenType number styles, kerning integrity, dash rendering, hanging-punctuation computation. The most detailed skill in the set. | Yes — reads/writes most `TextNode` properties |
| [`vertical-spacing`](./vertical-spacing/) | Margin/padding/Auto Layout gap against a grid base, vertical-trim optical correction, paragraph/list rhythm, Figma margin-collapse guard. | Yes — reads/writes `FrameNode` Auto Layout properties |
| [`type-scale-generator`](./type-scale-generator/) | Generates a font-size scale from a base size and ratio (8 named musical/geometric ratios, Fibonacci, classic Garamond steps), rounded to avoid subpixel rendering. | Optional — can check/write Figma text styles |
| [`glyph-fidelity`](./glyph-fidelity/) | All-caps tracking formula, ligature-collision guard under negative tracking, inline-acronym subrange treatment. Refines `text-typesetting`'s tracking output for specific edge cases. | Format-agnostic, applies equally to CSS |

## How they hand off to each other

```
type-scale-generator ──▶ text-typesetting ──▶ vertical-spacing
   (font sizes)         (line-height, tracking)   (rhythm, uses LH)
                              │
                    ┌─────────┴─────────┐
              glyph-fidelity      line-length-optimizer
          (all-caps/ligature        (column width,
           tracking edge cases)      feeds LH compensation
                                      back to text-typesetting)
                              │
                       microtypography
                (character-level: dashes, quotes,
                 widows/orphans — hands Figma
                 rendering decisions to text-typesetting)
```

Typical full pass: `type-scale-generator` → `line-length-optimizer` → `text-typesetting` (+ `glyph-fidelity` for all-caps) → `vertical-spacing` → `microtypography` last, since it depends on the column width and typeface choices made upstream.

## When to use the whole set vs. one skill

- **One skill**: a narrow, specific ask ("what line-height for this heading", "fix hanging conjunctions in this paragraph").
- **The full set in sequence**: setting up a new design system's type foundation, or auditing an existing Figma file end-to-end for typographic correctness.

## License

Each skill carries its own `LICENSE` (MIT) and `README.md`. See the individual skill folders for full authoring, references, and attribution.

---

*Part of the [Design Engineering Playbook](https://github.com/monikazapisekstudio/design-engineering-playbook) — AI-assisted workflow artefacts for product designers working in agile and lean environments.*
