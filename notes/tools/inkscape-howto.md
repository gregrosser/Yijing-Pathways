# Inkscape howto

Working notes from editing `dvisvgm`-exported SVGs in Inkscape for this
project.

## Making elements selectable

A single click with the Selection tool (S) usually grabs the whole
top-level group, since `dvisvgm` output is typically one big nested `<g>`
structure.

- **Alt+click** selects the actual object under the cursor, ignoring
  grouping. Alt+click again on the same spot cycles down through
  overlapping objects in z-order. Shift+Alt+click adds to selection this
  way.
- **Double-click** steps into a group one level at a time; **Esc** backs
  out.
- To permanently flatten: Ctrl+A (select all), then **Ctrl+Shift+G**
  (Ungroup), repeated — `dvisvgm` often nests groups several levels deep.
  Caution: this can flatten transforms/clip-paths into each element, and
  can break intentional sub-grouping (e.g. a letter "o"'s outer/inner
  subpaths). Ungroup one or two levels first and check before continuing.
- **Object → Objects...** panel shows the full tree; click a row to
  select that exact element on canvas.
- **XML editor** (Ctrl+Shift+X) shows the raw structure — also reveals
  whether text became `<text>`/`<use>` glyph references vs. plain
  `<path>` outlines (controlled by the `dvisvgm --no-fonts` flag, see
  [[dvisvgm-howto]]).

## Selecting multiple objects (Shift+click, not Ctrl+click)

Ctrl+click does **not** add to a selection in Inkscape, unlike the usual
OS convention (Explorer, Photoshop layers panel, etc.) — it selects a
single object under the cursor, ignoring group nesting, and **deselects**
whatever was selected before.

Use **Shift+click** to build a multi-object selection. Check the status
bar at the bottom ("N objects selected") before grouping. A one-object
group looks visually identical to no group at all, which is a common
cause of "I grouped two things and it looks ungrouped later" — really,
only one object was ever selected.

## Grouping objects into a group changes one object's stroke width

Cause: the two objects had different pre-existing scale transforms (e.g.
one was resized non-uniformly at some point). Inkscape's default
"Optimized" transform storage tries to bake transforms into path
geometry/stroke-width when grouping, which can misjudge non-uniform
scale and visibly change line thickness.

Fixes:
- **Edit → Preferences → Behavior → Transforms → Store transformation:
  Preserved** (instead of default "Optimized") — keeps transform matrices
  explicit instead of baking them into path/style data.
- Or flatten/reset the object's transform (e.g. Path → Object to Path)
  before grouping.
- Or just reset the stroke width numerically afterward in Fill & Stroke.

## "Paint is undefined" in Fill & Stroke

**Symptom:** an object is visibly colored on canvas, but Fill & Stroke
shows "Paint is undefined" for its fill or stroke.

**Cause:** the color isn't set directly on the object — it's inherited
from a parent `<g>` or a CSS class in a `<style>` block instead. Common
in `dvisvgm` output, which often sets `fill`/`stroke` once on a wrapping
group rather than repeating it on every path.

**Fix that worked (2026-08-15):** select all objects (Ctrl+A) and apply
a fill/stroke once (e.g. click a palette swatch). This writes an explicit
`fill`/`stroke` value directly onto every object, detaching them from the
inherited/CSS value.

To inspect the actual cause first: XML editor (Ctrl+Shift+X) → check the
object's own `style`/`fill`/`stroke` attributes, then its parent `<g>`,
then any `<style>` block in `<defs>` for a `class` reference.

## Moving a group into a separate layer

- **Layer → Move Selection to Layer...** — dialog lists all layers;
  create the target layer first via **Layer → Add Layer...** if it
  doesn't exist yet.
- **Shift+PageUp / Shift+PageDown** moves the selection to the
  layer directly above/below in the stack.
- Or drag the group's row in the **Objects** panel into the target
  layer's row.
- Note: layers are just `<g inkscape:groupmode="layer">` elements, so
  moving between layers can change stacking/z-order relative to other
  content — check the canvas after moving.

## SVG layers/groups in an HTML page

Relevant if exporting diagrams for interactive web use rather than (or
in addition to) Blender import.

- **Inline SVG** (paste `<svg>...</svg>` directly into the HTML body) —
  best option for interactivity. Layer/group `<g>` elements become real
  DOM nodes: target with CSS (`#layer1 { display: none; }`) or JS
  (`document.getElementById('layer1').style.display = 'none'`).
- `<object data="file.svg" type="image/svg+xml">` — loads as its own
  document but still reachable from the parent page via
  `object.contentDocument`.
- `<img src="file.svg">` or CSS `background-image` — **not interactive**;
  the SVG is isolated/rasterized, individual layers can't be targeted.
- Inkscape layers get `id="layerN"` automatically and an
  `inkscape:label` (a namespaced attribute, awkward to query from CSS/JS
  — prefer setting a plain `id`/`class` per layer before export if you
  plan to script against it).
