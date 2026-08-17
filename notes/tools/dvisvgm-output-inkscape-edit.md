# Prepping dvisvgm output for reuse in the diagram pipeline

Checklist for turning a raw `dvisvgm`-converted SVG (see
[[dvisvgm-howto]]) into something this project's data-driven diagram
generators can actually key off of — not just a static illustration.

## Why this step exists

`dvisvgm` output has zero semantic structure: every visual element
(circles, ellipses, glyphs) comes out as a plain `<path>`, usually
nested several `<g>` levels deep, with no meaningful `id`s. There's
nothing to bind data to — no `<ellipse>`/`<circle>`/`<text>` elements,
no groups matching the logical pairs/rings a reader actually sees.
Confirmed on `diagrams/FX-body-schema.svg`/`KW-body-schema.svg`: 74
and 73 raw `<path>` elements respectively, zero `<ellipse>`/`<circle>`
tags.

This matters when the goal is what came up first in the
`diagrams/spine/` renovation discussion: reusing the *style* of an old
PDF diagram (e.g. the "Fu Xi" body-schema's nested-ellipse, ink-on-paper
look) inside a page whose actual content is still generated from data
(the 64 numbered hexagram rows). Style-only reuse (backdrop image) needs
none of this; structural reuse (feeding real geometry into a generator)
does.

## The prep, in Inkscape (see also [[inkscape-howto]])

1. **Select all (Ctrl+A), Ungroup (Ctrl+Shift+G)**, repeated —
   `dvisvgm` nests groups several levels deep. Check after each pass;
   over-ungrouping can flatten transforms into path geometry.
2. **Manually re-group into meaningful units.** For this project's
   symmetric diagrams, that means binary groups of mirrored pairs
   (e.g. the two matching arcs of one nested-ellipse "ring") — the
   grouping a human recognizes by eye, not the grouping `dvisvgm`
   happened to emit.
3. **Rename each group's `id`** via the Objects panel or XML editor
   (Ctrl+Shift+X) to something legible — `ring-1`, `markers-top`, etc.
   — instead of leaving the auto-generated `g123`. This is the actual
   handle a script will key off of later.
4. Paths don't need flattening to primitives first — cx/cy/rx/ry (or a
   bounding-box center/extent) can be extracted from a path just as
   well as from a native `<ellipse>`, as long as each logical pair is
   isolated in its own named group.

## Status

As of 2026-08-17, this prep is done for `FX-body-schema.svg`: all 20
FX pair/quartet rings are grouped and labeled (`FX{a,a+1,b,b+1}`
format), and a further working copy (`FX-body-schema-layers-01.svg`)
carries all 64 hexagram numbers, each grouped with its circle
(fill-disc + stroke-ring + digit) under its own `id`. `KW-body-schema.svg`
has not had this prep applied yet — still raw dvisvgm output.

The `diagrams/spine/` → `spine02/` renovation pilot is underway on
page 1 (`Spine_Page1_FX.html`): the old bezier ribbon-bands have been
replaced with the literal body-schema geometry, numbered and
gray/black-filled per the "line 1 == line 6" / "line 1 != line 6"
convention used across the rest of the series. Pages 2-10 are still
untouched copies of the original ribbon style.
