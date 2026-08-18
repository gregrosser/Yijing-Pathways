<reading_instructions>
Whoever reads this document — a fresh Claude instance resuming this work, at the start of a new session — must lead their first response to the user with the contents of <current_todos> below, before summarizing <original_task>, <work_completed>, or anything else in this document.
</reading_instructions>

<current_todos>
# TO-DOS

## KW Body-Schema Master File Reconciliation - 2026-08-17 11:05

- **Reconcile `diagrams/KW-body-schema.svg` with `diagrams/KW-body-schema-nums.svg`** - the numbering, gray/black coloring, complementary-pair styling, and full 10-page spine rebuild are all done (spine pages are complete for now — see `diagrams/spine02/`). The one thing still open: `diagrams/KW-body-schema.svg` is an older ring-only master file (analogous to `FX-body-schema.svg`) that was modified by hand in Inkscape in parallel with the numbering work, which targeted the separate `diagrams/KW-body-schema-nums.svg`. Which file is canonical going forward — and whether `-nums.svg`'s ring/grouping edits should be back-ported to the plain master, or vice versa — hasn't been investigated or confirmed with the user. **Files:** `diagrams/KW-body-schema.svg`, `diagrams/KW-body-schema-nums.svg`. **Solution:** diff the two files' ring/group structure directly, decide with the user which is the source of truth for the ring geometry itself, and reconcile.

## XianTian Circle Diagrams & Hexagram Group Table - 2026-08-12 13:01

- **Show the logical/systematic design of the XianTian trigram circle** - Make the construction logic of the trigram circle visible to a reader, not just its arrangement. **Problem:** The trigram circle (hero SVG in `index.html`, and the original `diagrams/xiantian-trigram-circle.svg`) currently shows the 8 trigrams correctly positioned and color-coded (self-reversing pair vs. mixed pair via two cross-axes), but a reader can't tell *why* they're arranged this way just by looking — the binary/yin-yang line logic and the self-reversing/mixed grouping aren't explained. **Files:** `index.html` (hero SVG, trigram glyphs now drawn as precise rects), `diagrams/xiantian-trigram-circle.svg`, `diagrams/FuXi21.html`. **Solution:** consider annotating the two cross-axes directly (label what "self-reversing" and "mixed" mean structurally), and/or surfacing the binary line values (111/110/101/100/011/010/001/000) that drive each trigram's position.

- **Show how the XianTian trigram circle maps concentrically outward to the XianTian hexagram circle** - Build a new diagram showing the traditional concentric-ring construction: inner ring = 8 trigrams, outer ring = 64 hexagrams. **Problem:** no existing diagram in this project shows this mapping — it's a structural relationship central to the FuXi/XianTian sequence work but currently undocumented visually. **Files:** new diagram, most likely alongside `diagrams/xiantian-trigram-circle.svg` / `diagrams/FuXi21.html`; may draw on `data/spreadsheets/FX-01.ods` for FX hexagram ordering data. **Solution:** reuse the rect-based trigram glyph technique from `index.html`'s hero (font-independent, pixel-precise) for the inner ring; verify hexagram line patterns the same way they were verified for the trigrams (render and read directly, don't recall from memory) before drawing the outer ring.

- **Link the trigram circle and hexagram circle diagrams together** - Once both diagrams above exist, connect them as one coherent piece rather than two independent artifacts. **Problem:** not yet decided whether this means a single combined SVG, or two separate pages/entries cross-linked. **Files:** wherever the two diagrams from the items above end up (likely `diagrams/`), plus the "Structure" strand entries in `index.html`. **Solution:** decide the linking approach once both diagrams are built.

- **Rebuild the hexagram Group Table starting from a spreadsheet** - Redo the Group Table work, this time using a spreadsheet as the canonical starting data source rather than the prior approach. **Problem:** the existing `notes/structure/Group-Table-properties.md` needs to be reworked from scratch with a spreadsheet-first workflow. **Files:** `notes/structure/Group-Table-properties.md`, `data/spreadsheets/FX-01.ods`, `data/spreadsheets/FX-01.xml`. **Solution:** use `data/spreadsheets/FX-01.ods` (or a fresh spreadsheet, if that one isn't the right starting point) as the source of truth for regenerating the group table data and derived properties.

## Trigram Circles, 3D Cubes & Central Taiji Page - 2026-08-13 22:08

- **Build a graphical representation of the FX and KW trigram circles together** - Create a new diagram showing the FuXi (XianTian) trigram circle and the King Wen (HouTian/latter-heaven) trigram circle side by side or otherwise paired, analogous to `diagrams/FX_circle_KW_square.html`'s FX-hexagram-circle/KW-hexagram-square pairing built this session. **Problem:** no diagram in this project currently shows the two trigram orderings (FuXi vs King Wen arrangement of the 8 trigrams) together or in comparison — only the single FuXi trigram circle exists (`diagrams/xiantian-trigram-circle.svg`, and the hero SVG in `index.html`). **Files:** new diagram (likely `diagrams/fx-kw-trigram-circles.html` following this session's naming convention), `diagrams/xiantian-trigram-circle.svg` (existing FX trigram circle to reuse/extend), `index.html` (hero SVG has the established rect-based trigram-glyph rendering technique — reuse it rather than reinventing). **Solution:** the King Wen trigram arrangement (post-heaven/HouTian bagua) is a different, well-known traditional ordering from the FuXi (pre-heaven/XianTian) one used in this project so far — will need its own verified trigram-position data, sourced and cross-checked the same rigorous way the FX↔KW hexagram bijection was (see `notes/structure/FX_to_KW.md`), not assumed from memory.

- **Show how the yin/yang groups between the FX and KW trigram circles relate** - Once both trigram circles exist, add the same kind of group-highlighting/equivalence feature built this session for the hexagram FX circle ↔ KW square (click-to-highlight, matching color, `UNIFY`-style cross-link) — but for the 8 trigrams' yin/yang groupings rather than the 64 hexagrams' quartets/pairs. **Problem:** not yet designed — unclear exactly what "yin/yang groups" means at the trigram level in this project's terms (e.g. pure-yang/pure-yin trigrams vs. mixed ones, or the FuXi self-reversing/mixed cross-axis grouping already noted as unexplained in the pre-existing "Show the logical/systematic design of the XianTian trigram circle" TO-DO above). **Files:** whatever new diagram is built for the item above; `diagrams/FX_circle_KW_square.html` as the interaction-pattern reference (its `showGroup`/`clearGroup`/`HEX_TO_GROUP`/display-box/`UNIFY`-link machinery). **Solution:** resolve the pre-existing open question about the trigram circle's self-reversing-vs-mixed cross-axis grouping first (see the first item in the "XianTian Circle Diagrams & Hexagram Group Table" TO-DO section above), since that's likely the same "yin/yang group" structure this item wants surfaced and compared against the KW trigram ordering.

- **Create 3D cube representations of the trigrams, "à la Z.D. Yung"** - Build a new visual/diagram representing each of the 8 trigrams as a 3D cube. **Problem:** the specific reference ("Z.D. Yung") and exact cube convention intended is not yet clear from this conversation alone — needs clarification from the user before design work starts (e.g. whether it's a known published diagram/book the user has in mind, what axes map to which of the 3 lines, whether yang/yin lines become filled/open cube faces or vertices, etc.). **Files:** new diagram, likely `diagrams/trigram-cubes-3d.html`; may want CSS 3D transforms (`rotate3d`/`perspective`) or an SVG-based pseudo-3D projection consistent with this project's existing SVG-rect line-glyph technique rather than pulling in a 3D library/dependency. **Solution:** ask the user for the source/reference for "Z.D. Yung" and the intended cube convention before implementing, since guessing wrong here would waste a full design-and-build cycle.

- **Build a central-Taiji page linking FX trigrams ↔ FX digrams ↔ Taiji ↔ KW digrams ↔ KW trigrams** - New page with the Taiji (yin-yang) symbol at its center, flanked outward on one side by FX digrams then FX trigrams, and on the other side by KW digrams then KW trigrams. **Problem:** "digrams" (2-line figures, the 4 possible combinations of two stacked yin/yang lines) are a new concept not yet represented anywhere in this project — only trigrams (3-line, 8 combinations) and hexagrams (6-line, 64 combinations) exist so far, so the digram data/ordering (both FX and KW variants) needs to be defined and verified from scratch, the same rigorous way trigram and hexagram data has been throughout this project (derive and cross-check programmatically, don't hand-type). **Files:** new page, likely `diagrams/taiji-trigrams-digrams.html`; `index.html` hero SVG and `diagrams/xiantian-trigram-circle.svg` for the existing rect-based line-glyph rendering technique to extend down to 2-line digrams and up to reused 3-line trigrams. **Solution:** clarify with the user what "FX digrams" vs "KW digrams" actually means (KW's traditional sequence is normally defined at the trigram/hexagram level, not digram level — the FX/KW digram distinction may need to be derived by the user's own logic, not an existing classical source) before building; likely depends on the "yin/yang groups" work above being resolved first, since the whole point of this page is showing the progressive binary construction (Taiji → digrams → trigrams) symmetrically for both orderings.

## KW Square Distance Markers - 2026-08-14 14:15

- **Add counting markers and distance brackets to the KW square** - Give `diagrams/kw-square.html` the same per-group distance annotation that `diagrams/FX_circle_KW_square.html` already has on the FX circle side. **Problem:** `FX_circle_KW_square.html` draws, per selected group, counting markers plus a bracket between paired members showing their distance apart (`buildDistanceLink()` around line 1752, drawing into the `#distance-overlay` `<g>`, populated on `showGroup()` and cleared via `overlay.innerHTML = ''` in `clearGroup()` — see the `.distance-link`/`.distance-tick`/`.distance-label-bg`/`.distance-label-text` CSS around line 126). `kw-square.html` has no equivalent yet. **Files:** `diagrams/kw-square.html` (to build); `diagrams/FX_circle_KW_square.html` (reference implementation, `buildDistanceLink()` and the `showGroup`/`clearGroup` pop-up wiring). **Solution:** port the same show-on-select/clear-on-deselect behavior, but note the KW square is a square grid, not a circle — `buildDistanceLink()`'s arcs (`arcPath()`, `.distance-link` paths) don't apply directly. The KW brackets need to be **straight lines with tick marks** (not arcs) — keep the tick/label-bubble parts of the pattern, replace the arc geometry with line geometry appropriate to the square layout.
</current_todos>

<original_task>
Session opened with the top TO-DOS item: complete the KW body-schema numbering (carried in from a prior session, already largely resolved by the time this session's transcript begins — see `<critical_context>` for the very start-of-session state). From there the user drove an extended, tightly-iterative sequence of visual refinements to the FX/KW body-schema spine pages, culminating in an explicit instruction to rebuild the entire 10-page spine series using the two finished body-schema diagrams, followed by several rounds of layout-consistency fixes across all 10 pages, then session-end housekeeping (TO-DOS cleanup, whats-next refresh — this document). No single original task statement covers the whole session; each instruction below was a discrete, explicit user request, mostly building on the immediately preceding one.
</original_task>

<work_completed>

## 1. FX number-circle fill color (parity with prior session's KW fix)

Changed all 128 `NumCirc` fill-disc paths' `fill="#ffffff"` → `fill="var(--paper)"` in both `diagrams/FX-body-schema-layers-01.svg` (source) and `diagrams/spine02/Spine_Page1_FX.html` (embedded copy). Verified the plain `fill="#ffffff"` attribute occurs exactly 128 times in each file, exclusively on `NumCirc` fill-discs (confirmed via Python/lxml nearest-enclosing-group check on every occurrence — zero exceptions). Verified via before/after headless-Chromium screenshot: page background is `--paper:#f2ecdc` (cream, not pure white), so circles now visibly tint to match the page; a cropped pixel comparison confirmed digit position and ring geometry were pixel-identical (color-only change, zero layout regression).

## 2. Removed fill from the 8 "complementary pair" ring elements (both FX and KW)

The 20 ring/group elements in each body-schema SVG split structurally into 8 two-member "pairs" (single `<path>` or 2-path `<g>`, e.g. `FX{1,2}`) and 12 four-member "quartets" (`<g>` with 2 child `<path>`s, e.g. `FX{3,4,63,64}`). Per explicit instruction, stripped fill from all 8 pairs in both diagrams (`fill="none"` on the presentation attribute and in the `style` attribute, leaving quartets untouched) — done via a Python regex script scoped by element `id`, applied to `diagrams/FX-body-schema-layers-01.svg`, `diagrams/KW-body-schema-nums.svg`, and both embedded spine pages. Verified via screenshot: pairs render as thin outline rings, quartets remain solid filled bands.

## 3. Discovered and correctly resolved the `line1==line6` vs `line1≠line6` distinction within the 8 pairs

User asked to widen "the `line1==line6` complementary pairs" by 50%. Initial implementation (wrongly) widened all 8 pairs uniformly. Investigation using the project's own `HEXLINES` data (embedded in `diagrams/FX_circle_KW_square.html`) proved computationally that **all 20 ring groups** (not just pairs) split cleanly 10-gray/10-black by whether their member hexagrams have `line1==line6` — and further, that the 8 pairs themselves split exactly 4 `eq` / 4 `neq`:
- FX eq pairs: `{1,2}`, `{61,62}`, `{37,38}`, `{25,26}` (ids: `path55`, `path14`, `path24`, `path30` — all bare single-`<path>` pairs)
- FX neq pairs: `{43,44}`, `{15,16}`, `{51,52}`, `{23,24}` (ids: `g6`, `FX_15_16`, `g8`, `g2` — all `<g>`-wrapped pairs)
- KW eq pairs: `{1,2}`, `{61,62}`, `{29,30}`, `{27,28}` (bare-path ids `KW_01_02`, `KW_61_62`, `KW_29_30`, `KW_27_28`)
- KW neq pairs: `{63,64}`, `{53,54}`, `{17,18}`, `{11,12}` (`<g>`-wrapped ids `KW_63_64`, `KW_53_54`, `KW_17_18`, `KW_11_12`)

This eq/neq split also holds for all 12 quartets (verified computationally — each quartet's 4 members share the same `line1==line6` status), confirming the full 20-group gray/black table already documented from a prior session is exactly this classification.

Corrected sequence of stroke-width edits (all applied to both `style` and presentation attributes, in both source SVGs and both embedded pages):
- Reverted the wrongly-widened 4 neq pairs back to original, then to original×0.65 (user's requested "-35%" for the neq/black set).
- Kept the 4 eq pairs at their correctly-applied +50%.
- Fully reverted an intermediate (also-wrong) -35% stroke-width edit that had been mistakenly applied to all 12 quartets (user clarified quartets were never in scope).
- Final instruction: scale **all 8 pairs** (both eq and neq) a further ×1.35 from their then-current values, while explicitly preserving eq > neq. Final `style` stroke-width values: FX/KW eq = `2.025`, FX neq = `1.2285`, KW neq (before the next step) = `0.8775`.
- **Found and fixed a real cross-diagram inconsistency**: FX's and KW's neq pairs had diverged (`1.2285` vs `0.8775`) purely because their two source SVGs had different original baseline `style` stroke-width values (`1.4` vs `1.0`) baked in from whenever each was originally drawn — all the proportional scaling had preserved that original mismatch rather than closing it. Fixed by setting KW's 4 neq pairs' `style` stroke-width to `1.2285` exactly (matching FX), confirmed both `attr` and `style` now identical between the two diagrams for both eq and neq categories.
- **Also fixed FX's eq-pair width to match KW's**: found FX eq = `2.8532` vs KW eq = `2.025` (same root cause, different baseline). Set all 4 FX eq pairs' `style` **and** `attr` stroke-width to `2.025` (matching KW exactly, including `path30` which uniquely had no `style` stroke-width key at all — relies on `attr` alone).

All perceptual/visual verification methods used a "recolor gray to black" test render to rule out a genuine optical illusion where the lower-contrast gray tone visually reads as thinner even when numerically wider — confirmed this illusion was real and that the underlying geometry was correct throughout.

## 4. Resized FX and KW single-panel diagrams (pages 1/2) to matched height, +20% larger

User: "make the FX 20% larger and the KW equal to that new FX size." Computed exact geometry: FX viewBox `348×661` native units, KW viewBox `287×660`. Set FX's page container width formula from `min(1900px, 96vw)` → `min(2280px, 96vw)` (exactly +20% on the px cap; deliberately did **not** scale the `vw` term — see Attempted Approaches for why). Computed KW's matching width via the aspect-ratio ratio `(661/348)×(287/660) = 0.825962` so that KW's rendered height exactly equals FX's new height at any container width — initially applied as `min(1883.19px, 79.29vw)` (also correcting the same vw-scaling mistake). Verified via screenshot content-bbox measurement: FX and KW heights matched to within 0.14% (6px out of ~4200px).

This sizing formula was **later fully superseded** by the shared-grid-fraction formula from Work Item 8 below — see `<critical_context>` for the final, currently-live formula.

## 5. Fixed nav-arrow/caption horizontal centering bug on the (then still single-panel) FX/KW pages

Found via narrow-viewport screenshot that the diagram overflowed/clipped at viewports narrower than ~1979px because the `vw` term in the width formula (`115.2vw`, from a naive ×1.2 scaling of the original `96vw`) mathematically can never be satisfied without overflow (`Nvw` for any `N>100` always exceeds the viewport). Fixed by reverting the `vw` term to the original safe `96vw`/`79.29vw` (only the `px` cap should scale with "+20% larger" requests — the `vw` term is a narrow-viewport safety margin, not a size target). This was purely a page 1/2 CSS fix; superseded later by Item 8 below along with everything else in the sizing formula.

## 6. Built the full 10-page spine series on the new body-schema diagrams (major work item)

Pages 3–10 of `diagrams/spine02/` had never been touched since a prior session first swapped pages 1–2 onto the new dvisvgm body-schema diagrams — they still contained the old, unrelated hand-authored "ribbon" diagram (`viewBox="-583.22 -1.00 1218.44 2602.00"`). Investigated the old pages' design (via `diff`/`md5sum` against `diagrams/spine/` backups and content inspection) and found a clear, deliberate 2×5 structure:

| | With numbers | No numbers |
|---|---|---|
| FX alone | Page 1 | Page 6 |
| KW alone | Page 2 | Page 7 |
| FX + KW side by side | Page 3 | Page 8 |
| Only `line1==line6` groups | Page 4 | Page 9 |
| Only `line1≠line6` groups | Page 5 | Page 10 |

Confirmed via `HEXLINES`-based computation (not assumption) that the "only eq/neq groups" filtering works because all 20 ring groups (not just the 8 pairs) split cleanly 10/10 by `line1==line6` — filtered pages are exactly page 3/8 with 10 of the 20 ring groups removed, numbers always shown in full regardless of filter (confirmed by counting `num`/`num-self` circle elements across old page3/4/5 — identical count, only ribbon count halved).

Built a reusable Python extraction pipeline (in scratchpad `spine_build/extract.py` + `spine_build/build_pages.py`, **not committed to the repo** — scratch tooling only) that:
- Parses `FX-body-schema-layers-01.svg` / `KW-body-schema-nums.svg` via `lxml`.
- Extracts the 20 top-level ring/group elements (optionally filtered to only `eq` or only `neq` group labels, derived from hardcoded `FX_EQ`/`KW_EQ` label sets computed once via `HEXLINES`).
- Extracts the 128 `NumCirc` number-circle groups (optional, `with_numbers` flag; KW's live inside a `g1`/`NUMBERS` wrapper that must be unwrapped, FX's are flat top-level siblings).
- **Recolors** each ring element and every descendant `<path>` to the established gray/black convention (`var(--ink-faint)` / `var(--ink)`, `fill-opacity:0.8` for quartets) at extraction time — necessary because the *source* SVGs still carry raw `#000`/`#fff` colors; the gray/black recoloring has only ever been applied at the point of embedding into a spine page, never written back to the source files.
- Splices the extracted content into a page-specific HTML shell (single-panel shell reused/adapted from Page 1/2's existing structure; a new two-panel shell built from scratch, modeled on the old Page 3's `page-columns`/`panel`/`divider` CSS scaffold).

**Two real bugs were found and fixed during this build, both through direct verification rather than assumption:**
- The raw source SVGs use a **decoy `fill="none"` presentation attribute** on quartet paths, with the actual fill color set via `style="fill:#ffffff;..."` (style overrides attribute per CSS/SVG precedence) — an initial recolor pass wrongly treated the attribute as authoritative and left quartets unfilled. Fixed by checking `style`'s `fill:` value first, falling back to the attribute only when `style` has no `fill:` key.
- (Two more layout bugs found in Items 7 and 8 below, both surfaged by subsequent user reports.)

Two-panel pages use `grid-template-columns: 1fr auto 0.825962fr` (not equal `1fr auto 1fr` as the old page3 used) — this makes FX and KW panels render at **exactly matched height at any viewport width automatically** (since `0.825962 = (661/348)×(287/660)`, the same aspect-ratio-matching constant from Item 4), which is more robust than the old page's fixed-ratio equal-column approach.

All 8 new/rebuilt pages verified individually via screenshot (both light-mode rendering and narrow-viewport overflow checks) before moving on. Full nav-href chain (1→2→…→10→1) verified programmatically — intact.

## 7. Fixed pages 6/7 caption/nav not centered under the diagram

User-reported bug. Root-caused via a red-centerline-overlay screenshot technique (draw a vertical line at the exact pixel center of the screenshot, compare to visible diagram center) that the diagram itself *was* centered, but `.panel`'s children (`name-tag`, `h1`, indirectly `nav-row`) were left-aligned. Found the exact cause: the reusable single-panel HTML-generation template (`SINGLE_PANEL_CSS_TMPL` in the scratchpad build script) was missing the `.panel { display:flex; flex-direction:column; align-items:center; ...}` rule entirely — present in the two-panel template and in the original hand-authored pages 1/2, but never carried over when the single-panel template was written from scratch for pages 6/7. Added the rule, rebuilt, reverified with the same centerline-overlay method — fixed.

## 8. Fixed pages 1/2/6/7 diagrams rendering far larger than pages 3–10, throwing off nav-button position (major fix, superseded Item 4/5's sizing formula entirely)

User: "raise the images on pages 1,2,6 and 7 so that they render at the same area of the page as the rest." Investigated via a red-border-overlay technique on the *container* element (not just content pixels) and proved the container top position was byte-identical (`448px`, matching `body`'s `padding-top`) on every page — ruling out any "vertical offset" bug. The real cause: pages 1/2/6/7 used an independently-tuned `min(px, vw)` cap (from Item 4/5), while pages 3–10 size each panel as a fraction of the shared `--page-w` grid variable — these two formulas diverge substantially at typical desktop viewport widths (verified: at 1920px, page 1's solo diagram rendered ~2× the height of page 3's FX panel), pushing the name-tag/caption/nav far down the page on solo pages.

Fix: replaced the independent px/vw cap on `.single-panel-wrap--diagram` (pages 1, 2, 6, 7) with a `calc()` formula deriving directly from the same `--page-w`/`--page-gap`/`--page-divider` variables the two-panel grid uses, so a solo panel renders as exactly "one column" of the same implicit grid: `width: calc((var(--page-w) - 2 * var(--page-gap) - var(--page-divider)) * SHARE)`, where `SHARE = 1/(1+0.825962) = 0.5476565229725482` for FX and `SHARE = 0.825962/(1+0.825962) = 0.4523434770274518` for KW.

**A subtle bug was found and fixed within this same fix**: the first version of this formula used `(page-w - gap - divider)` (subtracting **one** gap), but the actual `1fr auto 0.826fr` grid has **three** tracks and therefore **two** gaps between them (`page-w - 2×gap - divider` is the correct available-space formula for `fr` distribution) — this was caught by comparing the corrected formula's predicted width against the *actually measured* rendered width of page 3's FX panel (805.6px predicted vs 813px measured, close; the original one-gap version would have predicted ~915px, clearly wrong). Fixed by adding the missing `2 *` before `var(--page-gap)`, matching the pattern already present in the pre-existing (unrelated) `.single-panel-wrap` (non-`--diagram`) rule, which had always had this correct.

Verified via `last content row` measurement (find the lowest non-background pixel across a full-page screenshot) at two different viewport widths (1920px, 1400px) — all 10 pages landed on the exact same row at each width, after this fix.

## 9. Fixed a residual viewport-dependent nav-position inconsistency between page3/8 and page4/5/9/10

After Item 8's fix, re-verification at 1400px viewport showed pages 3 and 8 (the "Both" pages) ending 35px lower than pages 4/5/9/10 (the eq/neq filtered pages) — despite Item 8's fix making everything else consistent. Root cause: page 3/8's `h1` text ("The Inversion Spine / The Complement Spine", long) wraps to 2 lines at narrower viewports while page 4/5/9/10's `h1` text ("line 1 == line 6", short) always stays on 1 line — a genuine, viewport-dependent height difference. Fixed by giving the shared `h1` CSS rule (applies to every page) `min-height: 2.4em; display:flex; align-items:center; justify-content:center;` — reserves a fixed 2-line-tall box regardless of actual text length/wrap, so `nav-row`'s position below it is now viewport-independent. Reverified at both 1920px and 1400px — all 10 pages match exactly at both widths (`2353`/`1812` respectively).

## 10. Fixed "double descriptions" on pages 3 and 8

User: both `<h1>` captions under page 3/8's FX and KW panels showed the *same* combined text "The Inversion Spine / The Complement Spine" duplicated under each panel, when each panel should show only its own single description. Root cause: `build_two_panel()` in the scratchpad script took one shared `h1_text` parameter, used identically for both panels — correct behavior for pages 4/5/9/10 (which legitimately show the same classification label under both panels, e.g. "line 1 == line 6"), but wrong for pages 3/8. Changed the function signature to `fx_h1_text`/`kw_h1_text` (two separate parameters), updated all 6 call sites: pages 3/8 now pass `"The Inversion Spine"` / `"The Complement Spine"` separately; pages 4/5/9/10 pass the same string twice (unchanged effective behavior, now explicit). Rebuilt, verified via screenshot crop of the caption area, and reverified full nav-position consistency across all 10 pages was undisturbed by the text change (it wasn't — `min-height` from Item 9 absorbed it).

## 11. Committed and pushed all of the above

`git add` on all 12 touched files (`TO-DOS.md` + `diagrams/FX-body-schema-layers-01.svg` + `diagrams/KW-body-schema-nums.svg` + all 10 `diagrams/spine02/Spine_Page*.html`), single commit `492e937` ("Rebuild the full 10-page spine series on the new FX/KW body-schema diagrams") with a detailed body covering items 1–9 above (item 10, the double-description fix, and item 12 below happened *after* this push — see `<current_state>`), pushed to `origin/master`. Confirmed via `git status` (clean) and the push output (`9752f17..492e937 master -> master`).

## 12. TO-DOS.md cleanup (this session, per explicit instruction: "the 'spine pages' are completed for now")

- Removed the "FX Num Fill Colour" section entirely (fully complete, no remaining work — was superseded by the much larger spine rebuild).
- Renamed/simplified "KW Body-Schema Numbering" → **"KW Body-Schema Master File Reconciliation"**: dropped the now-obsolete "numbering work is DONE" narrative (numbering, coloring, pair styling, and the full spine rebuild are *all* done now, a much bigger completion than the original note described), kept only the one genuinely still-open item — reconciling `diagrams/KW-body-schema.svg` (hand-edited ring-only master, modified in parallel by the user in Inkscape during a prior session, never investigated) against `diagrams/KW-body-schema-nums.svg` (the numbering working file, now canonical source for the spine pages).
- Left the three unrelated sections (XianTian Circle Diagrams & Hexagram Group Table; Trigram Circles, 3D Cubes & Central Taiji Page; KW Square Distance Markers) completely untouched — confirmed none of them relate to spine-page work.

**Not yet committed** — this is the immediate next action, see `<current_state>`.

</work_completed>

<work_remaining>

## Immediate — this session's own wrap-up (in progress as this document is written)

1. **Commit and push the TO-DOS.md cleanup (Item 12 above)** — not yet done. `git status` currently shows only `TO-DOS.md` modified (everything else was already committed/pushed in Item 11). This document (`whats-next.md`) is also new/modified and should be included in the same commit per this project's established closing pattern (TO-DOS update → whats-next refresh → git push, all as one commit).

## From TO-DOS.md (see `<current_todos>` above for full detail — this is the complete, current list)

1. **Reconcile `diagrams/KW-body-schema.svg` with `diagrams/KW-body-schema-nums.svg`** — the sole remaining open item from the KW numbering work; not investigated this session (flagged, not touched).
2. XianTian trigram circle — annotate the construction logic (binary/self-reversing vs mixed).
3. Trigram→hexagram concentric-ring diagram (inner 8 trigrams, outer 64 hexagrams).
4. Link the trigram circle + hexagram circle diagrams together.
5. Rebuild the hexagram Group Table from `data/spreadsheets/FX-01.ods` as canonical source.
6. FX/KW trigram circles paired diagram (needs verified King Wen trigram-position data, not assumed from memory).
7. Yin/yang group highlighting for trigrams (depends on item 2 being resolved first).
8. 3D trigram cubes "à la Z.D. Yung" — **needs user clarification** on the reference/convention before starting.
9. Central-Taiji digram/trigram linking page — **needs user clarification** on what "FX digrams" vs "KW digrams" means.
10. KW square distance-bracket markers (straight-line/tick version of the FX circle's arc distance markers).

## Not yet asked / open judgment calls

- Whether any of the 10 spine pages' dark-mode rendering has been verified in a real browser (headless-Chromium in this environment cannot reliably emulate `prefers-color-scheme`; Playwright MCP confirmed non-functional again this session, consistent with prior sessions). Not checked at all this session, for any page.
- The reusable Python extraction pipeline built this session (`extract.py`, `build_pages.py`) lives only in the ephemeral scratchpad directory (`/tmp/claude-1000/.../scratchpad/spine_build/`), **not saved anywhere in the repo**. If the spine pages need rebuilding again in the future (e.g. after further body-schema source-SVG edits), this pipeline would need to be reconstructed from scratch unless it's deliberately saved into the repo first. Not discussed with the user — worth raising if further spine-page regeneration seems likely.
- The stray leftover file `diagrams/spine02/Spine_Page1_FX-nums-noFill.html` (noted in a prior session's handoff as an intermediate/duplicate artifact, not part of the canonical 10-page nav chain) still exists and was not touched, deleted, or otherwise addressed this session.
- The orphaned white fill-disc `path283` in the KW source SVG (noted in a prior session as harmless, invisible white-on-white) was not revisited this session.

</work_remaining>

<attempted_approaches>

- **Naively widening/narrowing "the complementary pairs" without first checking eq/neq sub-classification** — wrong on the first attempt (widened all 8 pairs when only 4 `line1==line6` pairs were meant); corrected only after the user's follow-up instruction ("the others: line1≠line6 complementary pairs") revealed the oversight, at which point `HEXLINES` was consulted computationally to derive the exact split rather than guessing again.
- **Scaling both the `px` and `vw` terms of a `min(px, vw)` width formula uniformly when asked to make something "N% larger"** — wrong. The `vw` term is a narrow-viewport safety margin (must stay `<100`), not a size target; scaling it above 100 guarantees overflow on any viewport narrower than the px-cap's crossover point. Caught via narrow-viewport screenshot (content visibly clipped/overflowing to the right) after the user reported it as "not centred when zoomed in." Correct fix: only ever scale the `px` term; leave the `vw` safety margin at its original value (or, better — see next item — replace the whole formula with a percentage-based one that has no such failure mode at all).
- **Treating a raw SVG presentation attribute (`fill="none"`) as authoritative when recoloring, ignoring the co-present `style="fill:#ffffff"` attribute** — wrong; `style` always overrides presentation attributes per SVG/CSS precedence. This exact same class of bug had already been carefully handled for `stroke-width` earlier in the session (and in a prior session), but was initially reintroduced for `fill` when writing the new extraction pipeline from scratch — a reminder that this precedence rule needs re-application to *every* attribute pair independently, not just the ones previously debugged.
- **Assuming visual/perceptual thinness differences reflect the underlying numeric stroke-width correctly** — the gray (`var(--ink-faint)`) pair connectors visually *looked* thinner than the black (`var(--ink)`) ones even when numerically wider, due to a genuine low-contrast optical illusion (irradiation effect: high-contrast dark-on-light edges read as bolder). Resolved by rendering a color-neutral test copy (forcing `--ink-faint` to pure black temporarily) to isolate stroke-width from color-contrast — confirmed the numeric values were correct throughout and the illusion was purely visual, not a data bug. This method (temporarily neutralizing one visual variable to isolate another) proved reliable and is worth reusing for any future "X looks wrong but the numbers say otherwise" investigation.
- **Guessing at "why the images aren't centered/positioned the same" from CSS reasoning alone, without measurement** — repeatedly insufficient; the actual causes (container-vs-content bbox mismatch, missing `.panel` flex rule, gap-count-off-by-one in a `calc()` formula, h1 text-wrap height variance) were each different and non-obvious, and pure CSS-reading led to at least two wrong initial hypotheses before switching to a red-border/red-centerline pixel-overlay screenshot technique that gave an unambiguous, directly-measurable answer each time. This technique (inject a temporary bright-colored `border`/`outline` on the specific element in question, screenshot, find the colored pixels programmatically) is now the established, reliable method in this project for any "is X positioned/sized correctly relative to Y" question — prefer it over both visual-only inspection and CSS-reading-only reasoning.
- **Off-by-one gap count in a responsive `calc()` grid-fraction formula** — `(page-w - gap - divider)` vs the correct `(page-w - 2*gap - divider)` for a 3-track grid (2 gaps between 3 tracks). Caught only by comparing the formula's *predicted* pixel output against an *actually measured* rendered width (805.6px predicted vs 813px measured with the fix; ~915px predicted without it, clearly wrong) — a reminder to always cross-check a derived CSS formula against a real measurement, not just re-derive it more carefully on paper.

</attempted_approaches>

<critical_context>

## Start-of-session state (for context on what was already true before this session's transcript begins)

This session's transcript opens mid-way through prior work: the user asks to read `whats-next.md`, and the assistant (per persistent memory instructions) leads with the TO-DOS list, then notes that the prior handoff's "not yet committed" claim was stale — `git status` showed a clean tree, with commit `9752f17` ("Number the KW body-schema and renovate spine page 2") already pushed to `origin/master`. This confirms: KW body-schema numbering, digit alignment, and Page 2 renovation were **already fully complete and pushed** before this session's own work began. The user then asked to update the stale "KW Body-Schema Numbering" TO-DOS entry (done, locally, uncommitted at that point) before the FX/KW visual-refinement work (this document's Items 1–5) began.

## The eq/neq (`line1==line6`) group classification — load-bearing, re-derive-don't-recall

`HEXLINES` (embedded as JSON in `diagrams/FX_circle_KW_square.html`, `re.search(r'HEXLINES\s*=\s*(\{.*?\});', html, re.DOTALL)`) gives each FX-numbered hexagram 1–64 as a 6-element yin/yang array, **index 0 = line 1 (bottom), index 5 = line 6 (top)**. `line1==line6` is `lines[0]==lines[5]`. This splits all 64 hexagrams exactly 32/32. Applied to the 20 ring groups (both FX-native labels and KW labels translated via the `data-hex`/`data-kw` bijection in the same file), every single group is **homogeneous** — all members share the same eq/neq status — giving a clean 10 eq / 10 gray-colored groups and 10 neq / 10 black-colored groups. This is the same classification as the pre-existing "gray/black" color table documented in a prior session's handoff; this session confirmed computationally (not just recalled) that it is exactly the `line1==line6` property, and that it applies uniformly to quartets as well as pairs (not just pairs, as an early hypothesis this session wrongly assumed).

FX eq groups: `FX{1,2}`, `FX{61,62}`, `FX{37,38}`, `FX{25,26}`, `FX{29,30,57,58}`, `FX{13,14,49,50}`, `FX{45,46,53,54}`, `FX{9,10,17,18}`, `FX{5,6,33,34}`, `FX{21,22,41,42}`.

KW eq groups: `KW{61,62}`, `KW{29,30}`, `KW{27,28}`, `KW{37,38,39,40}`, `KW{31,32,41,42}`, `KW{25,26,45,46}`, `KW{21,22,47,48}`, `KW{9,10,15,16}`, `KW{7,8,13,14}`, `KW{1,2}`.

(The remaining 10 of each 20 are `neq`.)

## Exact final stroke-width/style values for the 8 pairs (as of end of session — don't recompute, verify against these)

- FX/KW eq pairs (both `attr` and `style` stroke-width): `2.025`.
- FX/KW neq pairs (`style` stroke-width; `attr` independently is `1.23651` on both, coincidentally already matching since both derive from the same universal `1.40912` default × the same chain of factors): `1.2285`.
- All 8 pairs have `fill="none"` (both attribute and `style`) — only the 4 `<g>`-wrapped neq/eq-mixed pairs' wrapper `<g>` elements may lack a `style` attribute entirely (e.g. `g2`/`FX{23,24}` in the source file) — this is original/expected, not a bug; their child `<path>` elements carry the real values.

## The extraction/recolor pipeline (this session's newly-built version — supersedes the "pipeline" described in prior sessions' handoffs, which only handled re-embedding into an *existing* hand-structured page, not building new page shells)

Lives in `/tmp/claude-1000/-home-greg-pCloudDrive-YIJING-Yijing-Pathways/c67f54bf-2df3-4738-84a9-50d1b525a149/scratchpad/spine_build/` — **this is a session-scoped scratchpad path and will not persist to a future session.** Two files:
- `extract.py` — `extract(svg_path, prefix, eq_set, with_numbers, group_filter, numbers_wrapper_id=None)` returns a string of concatenated, recolored SVG element markup (ready to splice into an HTML shell). `group_filter` is `None`/`'eq'`/`'neq'`. Internally calls `recolor(el, color)` which walks every descendant, checks `style`'s `fill:` value first (falling back to the `fill` attribute only if `style` has no `fill:` key) to correctly decide whether an element should stay `fill:none` (the 8 pairs) or get the full `fill:color;fill-opacity:0.8` treatment (quartets).
- `build_pages.py` — page-shell templates (`ROOT_CSS`, `TWO_PANEL_CSS`, `SINGLE_PANEL_CSS_TMPL`, `NAV_CSS`) plus `build_two_panel()`/`build_single_panel()` functions and the `if __name__=='__main__'` block that actually generates and writes all 8 files (3–10) directly to `diagrams/spine02/`. Re-running this script is fully idempotent/safe — it always regenerates all 8 files from the current state of the two source SVGs (`FX-body-schema-layers-01.svg`, `KW-body-schema-nums.svg`) plus the hardcoded `FX_EQ`/`KW_EQ` label sets.

**If this pipeline is needed again and the scratchpad is gone**, it can be fully reconstructed from the `<work_completed>` Items 6–10 descriptions above plus the exact CSS/formula values in this `<critical_context>` section — nothing in it depends on any external state beyond the two source SVGs and `FX_circle_KW_square.html`'s `HEXLINES`/bijection data.

## The current (final, live-in-repo) sizing formula for all 10 pages — supersedes Items 4/5's formula entirely

Both single-panel pages (`.single-panel-wrap--diagram`) and two-panel pages (`.page-columns`) now derive their width from the *same* three `:root` variables: `--page-w: min(4056px, 100%); --page-gap: 200px; --page-divider: 1px;`.

- Two-panel: `grid-template-columns: 1fr auto 0.825962fr; gap: var(--page-gap);` (3 tracks → 2 gaps consumed).
- Single-panel FX (pages 1, 6): `width: calc((var(--page-w) - 2 * var(--page-gap) - var(--page-divider)) * 0.5476565229725482);`
- Single-panel KW (pages 2, 7): `width: calc((var(--page-w) - 2 * var(--page-gap) - var(--page-divider)) * 0.4523434770274518);`

Where `0.825962 = (661/348)×(287/660)` (FX:KW height-matching ratio, from the two diagrams' native viewBox aspect ratios `348×661` and `287×660`), and the two `SHARE` constants are `1/(1+0.825962)` and `0.825962/(1+0.825962)` respectively — i.e. "what fraction of the 3-track grid's fr-space would this panel get if it were actually in that grid."

This formula is **entirely percentage-based** (no raw `vw` units anywhere) — inherently immune to the overflow failure mode from Item 5 above, since `100%` always resolves against the actual available parent width regardless of viewport size.

Also: shared `h1` rule (all 10 pages) now has `min-height: 2.4em; display:flex; align-items:center; justify-content:center;` — do not remove this without re-verifying nav-row position consistency across all 10 pages at multiple viewport widths (it exists specifically to absorb text-length/wrap variance between pages).

## Screenshot/verification techniques established or reconfirmed this session

- **Red-border/red-centerline overlay**: inject a temporary `border`/`outline: Npx solid red;` (via a Python string-replace on a *copy* of the HTML file, never the real file) onto the specific CSS rule/element in question, screenshot, then programmatically find red pixels (`(im[:,:,0]>180)&(im[:,:,1]<80)&(im[:,:,2]<80)`) to get an exact, unambiguous pixel position — far more reliable than either eyeballing or pure background-color-diff thresholding for "is X aligned with Y" questions. Used repeatedly this session (container top-position check, svg bounding-box measurement, centerline-vs-content check).
- **Color-neutralization test render**: to check whether a stroke-width difference is real or a color-contrast illusion, temporarily replace one `--ink-faint`/`--ink` CSS variable definition with the other's exact value (or with pure black) in a scratch copy, screenshot, and compare — isolates geometry from color perception.
- **Background-color-diff bounding-box scan** (`np.abs(im.astype(int)-bg).sum(axis=2) > threshold`) is useful for coarse "where does content start/end" questions but is **unreliable for precise/exact-pixel comparisons** — it merges unrelated content when not carefully x/y-restricted to a single element's own region first (this caused a real measurement mistake mid-session — see Attempted Approaches), and it's sensitive to the arbitrarily-chosen `threshold` value. Prefer the red-overlay technique whenever exactness matters.
- Environment notes reconfirmed from prior sessions, unchanged: `chromium-browser --headless --disable-gpu --no-sandbox --screenshot=<path> --window-size=<W>,<H> file://<absolute-path>` is the working screenshot command; **must write HTML/output files to `$HOME`, not nested scratchpad paths** (Chromium read/write failures there, confirmed again this session); Playwright MCP remains non-functional (not re-tested in depth, carried forward as known-broken).

## User's demonstrated preferences (this session, worth carrying forward)

- Extremely precise, terse, iterative feedback — single-sentence bug reports ("the names are not centred under the images") with no diagnostic detail included, trusting the assistant to investigate and find the exact root cause rather than guessing at a fix. Every single bug report this session had a real, specific, non-obvious root cause (never a red herring) — always investigate empirically (screenshot/measure) before proposing a fix, per this project's standing "verification over eyeballing" preference.
- Comfortable pointing out when an assistant's own hypothesis is wrong very tersely ("you're on the wrong track. this edit applies only to the ... this edit does not apply to quartets.") — expects the assistant to immediately drop the wrong hypothesis and re-derive from data rather than defend or partially salvage it.
- Explicit, minimal confirmation of large multi-step work ("looks good, another edit:") before immediately moving to the next request — does not need extensive summary/ceremony between steps, just correctness.
- For a substantial, ambiguous-scope task (rebuilding 8 pages), the user responded well to being asked a scoping question up front (via `AskUserQuestion`) rather than the assistant silently guessing at scope — chose the most comprehensive option ("Yes, all 8 pages") when offered.
- Standard session-end pattern reconfirmed once more this session: "clean up the to-do list [criterion]" → (this document) "refresh the whats-next" → (next, presumably) "push to master" — same three-step closing ritual as prior sessions, just issued as separate short instructions rather than one combined sentence this time.

</critical_context>

<current_state>

## Git — mostly committed and pushed; one small piece remains

`origin/master` is at `492e937` ("Rebuild the full 10-page spine series on the new FX/KW body-schema diagrams") — this covers Items 1–9 of `<work_completed>` (all FX/KW pair styling, sizing, and the full 8-page spine rebuild through the nav-position and h1-height fixes). Confirmed via `git log` and the push command's own output.

**Note on chronology**: within the session, Item 10 (the "double descriptions" fix on pages 3/8) actually happened *before* Item 11 (the commit/push) — the numbering above reflects a drafting slip, not the real order. Confirmed directly (`git show HEAD --stat`): `Spine_Page3_Both.html` and `Spine_Page8_Both.html` are both present in commit `492e937`, so the double-descriptions fix is correctly included and pushed. No ambiguity remains.

**Not yet committed** (confirmed via `git status --short` just now):
```
 M TO-DOS.md
 M whats-next.md
```
This is Item 12 (the TO-DOS cleanup) plus this handoff document itself.

## Immediate next step

1. Stage and commit `TO-DOS.md` and `whats-next.md` — the user's established closing pattern strongly suggests they will next say "push to master" or similar.
2. Push to `origin/master`.

## Deliverable status

All 10 spine pages (`diagrams/spine02/Spine_Page1_FX.html` through `Spine_Page10_Line1ne6.html`) are **complete and internally consistent** as of this session's work — matched diagram scale, matched nav-button position, correct per-panel captions, correct eq/neq group filtering, correct gray/black coloring, correct complementary-pair fill/stroke-width styling. This was explicitly confirmed complete by the user ("the 'spine pages' are completed for now") before moving to TO-DOS cleanup. No further spine-page work is expected in the immediate term; the TO-DOS list has been updated to reflect this (only the KW master-file reconciliation item remains from that whole thread of work).

</current_state>
