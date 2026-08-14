# Design System — PDF Collection

Extracted from 13 PDF books/notes accumulated over several years (`collectionPDFs/`), covering Yijing sequence comparison, Daoist body-mapping, and the Yijing-Modes music project. Method: rendered 457 pages to PNG (100dpi) and pushed them into 13 corresponding Figma files for visual reference (one file per source PDF, in the "Yijing pathways" team drafts — see links at the bottom); analyzed embedded fonts directly from the PDFs (`pdffonts`) and dominant colors via pixel sampling across the rendered pages. This document is a description of the *existing, organically-formed* visual system, not a proposed one — useful as a baseline before designing anything new on top of it.

## 1. Typography

All 13 documents are LaTeX output and share one typeface family throughout — this is the single strongest "brand" signal in the collection.

| Role | Font | Notes |
|---|---|---|
| Body text, titles, labels, captions | **URW Palladio L** (Roman, Bold, Italic, BoldItalic) | A Palatino clone — humanist old-style serif. Used for 100% of running text, table content, and diagram labels across every document. |
| Math notation | Computer Modern (CMR10, CMSY10, CMMI10) + AMS symbols (MSAM10, MSBM10) + PazoMath (incl. blackboard bold) | Appears in the more technical sequence-comparison documents (`FX-KW-*`, `The-King-Wen-Sequence`). PazoMath is a Palladio-matched math companion, so math and body text sit together cleanly. |
| Music notation | MusiXTeX (musix20, musixspx, TeXMUSIX16, TeXMUSIX20) | Found in `The-King-Wen-Sequence.pdf`, `The-Yijing-Modes.pdf`, `Yijing-Modes-4096.pdf` — confirms these contain typeset musical scores. |
| CJK (Chinese characters) | SimSun | `The-Yijing-Modes.pdf` only. |
| Symbols/dingbats | MarVoSym, wasy9/wasy10/wasyb10 | Miscellaneous annotation glyphs, used sparingly. |
| Sans/mono (rare) | Latin Modern Sans (LMSans10), Latin Modern Mono (LMMono10) | `The-Yijing-Modes.pdf` only — likely code/data callouts distinct from body serif. |

**Takeaway:** the typographic identity is a single, consistent humanist serif (Palladio) for everything a reader sees, with purpose-built companion fonts (math, music, CJK) brought in only where the content requires them. There is no sans-serif UI layer — this is a print/paper-first system, not a screen-UI one.

## 2. Color

Sampled 457 rendered pages (quantized to 24-unit RGB buckets, near-white/near-black excluded from "accent" counts).

**Overall: 89.1% near-white, 0.4% near-black, 10.4% everything else** (mostly midtone grays). This is a monochrome, ink-on-paper system — color is the exception, not the rule.

### Base (used everywhere)
- Page: white / off-white
- Text and line art: black

### Grayscale ramp (table rules, shading, hatch fills)
A consistent ~9-step gray scale, in roughly 24-unit increments:

`#D8D8D8` `#C0C0C0` `#A8A8A8` `#909090` `#787878` `#606060` `#484848` `#303030`

### Accent palette (diagrams only — never in body text)
A small qualitative set used to color-code categorical groupings in relationship diagrams (e.g. the FuXi/King-Wen quartet-and-pair diagrams):

| Swatch | Hex | Approx. RGB | Where seen |
|---|---|---|---|
| 🔴 | `#F03030` | 240,48,48 | `02-schematic`, `01pathEquiv*` (annotation/highlight red) |
| 🟠 | `#F09000` | 240,144,0 | `02-schematic` |
| 🟢 | `#187848` | 24,120,72 | `02-schematic` |
| 🟢 (yellow-green) | `#A8D818` | 168,216,24 | `The-King-Wen-Sequence` |
| 🔵 | `#3090F0` | 48,144,240 | `02-schematic`, `sequence-overview-08` |

This is the same four-color categorical logic later carried into the live project's spine/ribbon diagrams (`FX_spine_2tone.html` etc.) — i.e. the accent palette predates and directly informs the current diagram work in this repo.

## 3. Layout & composition patterns

### Title pages
Every book opens with a plain LaTeX `\maketitle`-style page: bold Palladio title horizontally centered, positioned about 30% down the page; author name ("Greg Rosser") in regular Palladio below it, smaller and more lightly spaced; the remaining ~60% of the page left blank. No cover art, no rules, no color — purely typographic.

### Diagram pages (e.g. `02-schematic`)
Circular/radial layouts: two concentric rings of numbered circular nodes connected by straight or curved spokes, each node color-coded via the accent palette (fill + contrasting ring border = two-channel color coding for overlapping categories). Diagrams are typically placed in the upper half of the page with the lower half left blank — these read as working notes rather than finished print spreads.

### Dense tabular/relational pages (e.g. `FX-KW-hex-table-full`)
A single-column vertical list of rows, each row: a small circled index badge (left, on a dotted leader line) → text label → up to four stacked hexagram-line glyphs (solid bar = yang, split bar = yin) → a second text label → a boxed count badge (right). Hierarchical relationships between rows are shown via dotted tree-branch connector lines and horizontal indentation, with an inline axis label (e.g. "FX(31,32) — AXIS OF SYMMETRY") anchoring the tree. A small rounded-rectangle "tag" label (e.g. "line 1 = line 6") appears at the page foot as a categorical footnote. Page numbers are centered, plain, unadorned, at the bottom margin.

## 4. Recurring components (the closest thing to a "component library" here)

- **Circle badge** — thin-stroke circle containing a small serif numeral. Used for cross-reference indices in both diagrams and tables.
- **Rounded-rectangle badge** — used for count/tag values (distinct from the circle badge, so shape itself carries meaning: circle = identity/index, rounded-rect = count/category tag).
- **Dotted leader/connector line** — links a badge to its row or shows tree-hierarchy relationships; consistently dotted (never solid or dashed) across every table page inspected.
- **Stacked hexagram-line glyph** — solid black bar (yang) vs. a bar split by a white gap (yin), stacked in groups of 3 or 6, used identically everywhere hexagrams are drawn.

## 5. Reading this visually

Each PDF was imported page-by-page into its own Figma design file (one per book, so no single file became unwieldy). Full page ranges per the agreed scope: 10 short documents in full; `00-DAOIST-BODY-MAP` (93pp) and `The-King-Wen-Sequence` (147pp) in full; `The-Yijing-Modes` pages 1–140; `Yijing-Modes-4096` pages 1–50.

| Source PDF | Figma file |
|---|---|
| 00-DAOIST-BODY-MAP.pdf | https://www.figma.com/design/uRQEGsr8QIGH2VdltpWDW1 |
| 01-yijing-intro.pdf | https://www.figma.com/design/NYHrXyWlPgMwwNVY3Wu75d |
| 01pathEquiv-dantians.pdf | https://www.figma.com/design/4YECzGgEb6I4MTZQdhOtXJ |
| 01pathEquiv-pg1and2.pdf | https://www.figma.com/design/pY2mdRSgn9hntvyiAqxCut |
| 01pathEquiv.pdf | https://www.figma.com/design/OOg0DWoYvtSsEevyxrU0Qy |
| 02-schematic.pdf | https://www.figma.com/design/dU6fsT474xAHD2aIitbJaN |
| FX-KW-body-schemas.pdf | https://www.figma.com/design/sVQsp2vxRPRDg2vyzEfI6L |
| FX-KW-hex-table-full.pdf | https://www.figma.com/design/0HdzIIndH7M2ctl0mFQvYu |
| FX-KW-hex-table.pdf | https://www.figma.com/design/TAQzVenZhLlJ8Fm2BUyTZJ |
| sequence-overview-08.pdf | https://www.figma.com/design/nE5qp9LSRGBd0RK9yVb7i1 |
| The-King-Wen-Sequence.pdf | https://www.figma.com/design/yUgatyBUmtoZvPHLy10QcH |
| The-Yijing-Modes.pdf (p1–140) | https://www.figma.com/design/mhihtlWJvBeAg7o72hZFNW |
| Yijing-Modes-4096.pdf (p1–50) | https://www.figma.com/design/eNOngf7Xjjx9AwgAu3aUN7 |

There is also an overview file created at the start of this pass, `PDF Collection Design Reference` (https://www.figma.com/design/ODWz0oFujC0DrgwyMAO7aq), currently empty of content — it can be used as an index/landing file linking out to the 13 books above, or removed.
