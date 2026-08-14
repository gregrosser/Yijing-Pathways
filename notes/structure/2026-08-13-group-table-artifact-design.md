# Group Table Artifact — Design

Replaces the Claude Artifact linked at the top of `Group-Table-properties.md`
with a new one that draws each hexagram as a glyph icon (reusing the site's
existing bar-glyph technique) instead of a bare FX number.

## Scope

- Covers Block 1 of `data/spreadsheets/FX-01.ods` only — the 10-row
  FX(31,32)/FX(33,34) Group Table. The KW cross-reference block and the
  `n`/`cuo(n)` table are out of scope for this artifact.
- Static table for now. No hover/click interactivity — but glyph elements
  carry `data-hex="N"` so it can be added later without restructuring.

## Data pipeline

Source of truth is `diagrams/FuXi21.html`, not a re-derivation:

- **Line patterns**: extracted from `glyph-N` / `glyph-outer-N` SVG groups —
  one `<line>` per `data-line` = solid yang, two `<line>`s = broken yin.
  Verified against a handful of `<title>` tooltips (e.g. `glyph-1` = "Qian
  90°") and cross-checked that all 64 FX numbers appear exactly once with no
  omissions.
- **Row/axis/pairing structure**: taken directly from `FuXi21.html`'s
  embedded `GROUPS` array (`distance`, `dual`, `pairs`, `axis` per group) —
  already confirmed to match every row currently in
  `Group-Table-properties.md`'s raw table.
- A one-off extraction script does this parsing; it's a build step only, not
  shipped with the artifact.

## Artifact

- New file: `diagrams/group-table.html` (canonical local copy, same pattern
  as `index.html` / `FuXi21.html`), published as a new Claude Artifact.
- Visual language: site design tokens from `design.md` (`--paper`, `--ink`,
  `--ink-soft`, `--rule`, `--structure`), light/dark/system-aware — not
  `FuXi21.html`'s own separate palette.
- Layout: 10 rows × 2 columns ("AXIS — FX(31,32)" / "AXIS — FX(33,34)"),
  each cell showing:
  - a `dist` badge (small circular badge, `--structure` color)
  - hexagram glyphs (6 stacked rects each, extending the hero SVG's 3-line
    trigram rect technique to 6 lines) with the FX number in mono type
    beneath each
  - quartet cells (4 members) grouped visually as two sub-pairs per
    `GROUPS[i].pairs`, with a gap between the pairs; pair-row cells (2
    members) sit side by side

## Integration

- `notes/structure/Group-Table-properties.md`: swap the artifact link at
  top for the new URL; add a line noting the table is confirmed against
  `data/spreadsheets/FX-01.ods` and glyphs are sourced from
  `diagrams/FuXi21.html`. Observations text is unchanged (same underlying
  numbers).
- `index.html`: convert the "Group Table Properties" entry from an unlinked
  `<div class="entry">` to `<a class="entry"
  href="file:///home/greg/pCloudDrive/YIJING/Yijing-Pathways/diagrams/group-table.html"
  target="_blank" rel="noopener">`, meta label changed from `Note` to
  `Diagram · local` (matching the FuXi Circle card).

## Verification

- Extracted line patterns cross-checked against `FuXi21.html`'s own
  `<title>` tooltips and confirmed all 64 FX numbers present exactly once.
- Headless-Chromium screenshot of the finished artifact before publishing
  (disposable copy if any transition/animation needs neutralizing first),
  to catch glyph rendering/alignment issues before shipping — same
  discipline used for the hero SVG centering fix.

## Note on process

This project has no git repo (confirmed in `whats-next.md`), so this spec
is saved directly under `notes/structure/` rather than
`docs/superpowers/specs/`, and there is no commit step.
