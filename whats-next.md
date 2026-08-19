<reading_instructions>
Whoever reads this document — a fresh Claude instance resuming this work, at the start of a new session — must lead their first response to the user with the contents of <current_todos> below, before summarizing <original_task>, <work_completed>, or anything else in this document.
</reading_instructions>

<current_todos>
# TO-DOS

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
This session opened with the user asking to read `whats-next.md` (the handoff from the prior session). The prior handoff itself was found to be stale by 5 commits (repo had moved on: KW-body-schema reconciliation, a spine03 fork, and KW-square distance markers had all landed and been cleaned out of `TO-DOS.md` since that document was written) — this was reported to the user up front, with the corrected/current TO-DOS list.

All substantive work this session was a long, iterative series of small, precise UI-refinement requests against a single file, `diagrams/FX_circle_KW_square.html`, each building on the last:
1. Reduce/resize the gap and font-size of the "FX Circle"/"KW Square" panel titles relative to their diagrams (150% of a hexagram's height; titles 100% larger).
2. Raise the FX circle (it was "too low"), reduce its title gap further, and horizontally... (actually vertically) align the FX circle's and KW square's visual centers.
3. Add a new, not-yet-built "FX_spine & KW_spine" page connection: keep the existing "UNIFY" link (renamed "TO TABLE", later "→ TABLE", later "TABLE"), moved lower; add a new two-line link box above it ("TO FX SPINE"/"TO KW SPINE", several text/arrow iterations later just "FX SPINE"/"KW SPINE").
4. Precisely align the new link box to the hexagram glyphs in the pair-display box, and the "TABLE" box's bottom edge to the *actual visual bottom* of the distance-bracket SVGs (not just their invisible bounding box).
5. Various fast iterative tweaks: unicode arrow → then removed again; arrow/box size changes; border/line-width doubling on the new link box; box-raise-by-percentage adjustments.
6. Rename the panel titles to "Fuxi circle" / "King Wen square" (still rendered upper-case via existing `text-transform: uppercase`).
7. Add mouse-hover highlighting: hovering over either half (inner or outer trigram) of an FX hexagram on the circle highlights the *whole* hexagram (both halves) in the structure accent color.
8. Precisely center both panel titles over the true visual centers of their diagrams (not just over their grid-column box, which for the KW square was offset 20px from the square's real visual center due to asymmetric CSS padding).
9. Finally, "refresh the to-do list" — i.e., produce this handoff document (this session did **not** modify `TO-DOS.md`; it is unchanged from the start of the session, verified via `git status` showing only `diagrams/FX_circle_KW_square.html` as modified).
</original_task>

<work_completed>

## Session-opening staleness check (no file changes)

- Read `whats-next.md` as it existed at session start, led with its `<current_todos>` per standing instruction.
- Ran `git status --short`, `git log --oneline -5`, `git diff --stat` and found the working tree **clean** and `HEAD` already 5 commits past what the stale handoff described (`6f61fff Add matching distance brackets under each pair-display box`, `7bc9dc9 Add KW square distance tokens/bracket and FX circle refinements`, `1ae0e63 Remove completed Spine03 section from TO-DOS.md`, `9094776 Reconcile KW-body-schema.svg pair-group styling with -nums.svg`, `1fad6d3 Fork spine03 with FX and KW eq/neq comparison pages, repoint index link`).
- Read the actual current `TO-DOS.md` (shorter than the stale handoff's version — the KW-body-schema-reconciliation and Spine03 items had already been completed and removed) and reported the corrected, current list to the user as the session's first substantive message. This confirmed, yet again, the project's standing "handoff docs can lag real repo state" pattern (`feedback_handoff-staleness-check` memory).

## All further work: `diagrams/FX_circle_KW_square.html` iterative UI refinement

All changes verified computationally via a headless-Chromium/Playwright measurement harness set up in the scratchpad directory (`/tmp/claude-1000/.../scratchpad/pw/`, using `playwright-core` + system `/usr/bin/chromium-browser`, since no network-installed Playwright browser was available) — **not eyeballed**, consistent with the project's `feedback_verification-standard` memory. Numbered measurement scripts (`measure.js` through `measure18.js`, `solve.js`, `minitest.js`, `shot.js`) were written throughout to extract precise `getBoundingClientRect()` / `getBBox()` values before and after each change, iterating pixel offsets until exact (sub-pixel) alignment was confirmed, then re-screenshotting for visual sanity checks. These scripts are scratchpad-local and will not survive to a fresh session (see `<work_remaining>`/`<critical_context>` for what to reconstruct if needed).

### 1. Panel-title sizing and gap-to-diagram (first request)
- `.panel-title` font-size: `0.78rem` → `1.56rem` (exactly 2×).
- Established **"one hexagram's rendered height" = 32px** as the project's reference unit for this file, taken from the file's own `.hex-glyph` (`viewBox="0 0 30 32" width="30" height="32"`) — used repeatedly as the basis for "150%", "40%", etc. instructions throughout the session.
- FX gap (title bottom → visible top of the SVG ring content, measured via the `<svg>`'s `getBBox()`, not the outer stage box) reduced from a measured 60.6px to exactly 48px (150% of 32px) via `.fx-diagram { margin-top: -12.6px; }`.
- KW gap (title bottom → first visible `.hex-glyph` in the grid) was originally 138.8px because `.diagram { align-self: center; }` (a shared rule) was vertically centering the shorter KW square inside the same (taller, circle-height-driven) grid row as the FX circle. Fixed by overriding `.kw-diagram { align-self: start; margin-top: 22px; }`, landing the gap at exactly 48px too.

### 2. "FX circle too low" / gap-reduce-further / center-alignment (second request)
- Diagnosed why simply shrinking the FX gap couldn't by itself align the two diagrams' vertical centers: the FX circle's actual visible ring content is ~636px tall (bbox height, not the 717.6px stage box) vs. the KW square's fixed 480px grid — aligning centers with both gaps shrinking is mathematically impossible without one growing, since `gap_KW = gap_FX + (halfHeight_FX − halfHeight_KW)` for a shared title baseline.
- Chose FX gap = 16px (`.fx-diagram { margin-top: -44.6px; }`) and let the alignment math set `.kw-diagram { margin-top: 74.2px; }` (empirically solved, then hand-verified — see `solve.js`), landing both diagrams' true visual vertical centers at the same Y-coordinate to within 0.02px.
- **Explicitly flagged to the user** that this necessarily grew the KW-side gap to ~100px (an unavoidable consequence, not a mistake) — user accepted this ("that looks good").

### 3. New "spine" navigation links (third request)
- Renamed `#unify-link` text `UNIFY` → `TO TABLE` (later iterations: `→ TABLE`, then `TABLE` — arrows were added and then explicitly removed in a later request).
- Added a new sibling element, `<div class="spine-link-group" id="spine-link-group">`, directly after `#unify-link`, containing two `<a>` children (`#spine-link-fx`, `#spine-link-kw`) — a single bordered box (`border-radius: 6px`, `overflow: hidden`) internally divided by a `border-bottom` between the two lines, so it reads as "two boxed lines inside one outer box" per the user's literal spec.
- Both new links point to a **placeholder, not-yet-created page**: `href="FX_KW_spine.html#fx"` / `href="FX_KW_spine.html#kw"`, `target="fx-kw-spine"`. This filename is **not confirmed with the user** — chosen only as a reasonable placeholder matching this file's own naming convention. **The page `FX_KW_spine.html` does not exist anywhere in the repo.**
- JS: `clearGroup()` and `showGroup()` updated to toggle `.active` on `#spine-link-group` in lockstep with `#unify-link`, so the new box only appears/positions when a hexagram group is selected (same show/hide lifecycle as the renamed table link).
- `positionUnifyLink()` (function name unchanged despite the renames) rewritten repeatedly across the session; **final version** (see exact current code in `<critical_context>`) computes:
  - `centerX` — unchanged formula, midpoint between the fx/kw pair-display boxes.
  - Spine-box Y — vertically centered on the actual `.pd-glyph` hexagram glyphs inside the pair-display boxes (averaged fx/kw), **not** an arbitrary offset.
  - Table-box Y — its bottom edge aligned to the *actual drawn bottom* of the distance-bracket SVGs, found via `getBBox()` on the SVG's own content (the naive `getBoundingClientRect()` of the outer `<svg>` was ~21px too low, because the bracket's tick-marks render near the *top* of a fixed 40px-tall SVG box, leaving blank space below — this was a real, non-obvious bug caught only by bbox measurement, matching a "reduce the gap further" user complaint that turned out to have a structural cause, not just a wrong constant).
  - A **40%-of-own-height raise** was layered on top of the bracket-bottom alignment per a later request (`unifyLink.style.top = distanceBottom - unifyHeight/2 - unifyHeight*0.4`) — this is dynamic/relative to the element's *current* rendered height, so it automatically tracks later font-size/content changes (confirmed: when arrows were later added then removed, the 40% raise amount changed automatically with the box's height, without needing a code change).

### 4. Arrow icon iterations (fourth and fifth requests — net effect: no arrows in current file)
- Added a real Unicode arrow (`&#8594;` / `→`) replacing a literal `->` typed by the user in the previous round, applied to all three link labels.
- Enlarged just the arrow character via a `<span class="link-arrow">` at `font-size: 2em` (100% larger than surrounding text) — this transiently inflated box heights, which (via the height-relative 40%-raise formula above) caused a real ~7.8px overlap between the "spines box" and the "TABLE" box; **flagged explicitly to the user** rather than silently patched, since the exact desired inter-box spacing hadn't been specified.
- User's next request removed the arrows **entirely** ("remove the arrows altogether") — the `<span class="link-arrow">` wrappers and the arrow glyphs themselves were deleted from all three links, and the now-dead `.link-arrow` CSS rule was removed. Confirmed via measurement that box heights reverted exactly to their pre-arrow values (33px / 65px) and the overlap resolved itself as a side effect (16px clean gap).

### 5. Border/line-width matching (sixth and seventh requests)
- User asked to match the "spines box" line-width to the distance-bracket's SVG `stroke-width: 1.5`. Implemented `border: 1.5px solid var(--structure)` (outer) and `border-bottom: 1.5px solid var(--structure)` (internal divider).
- **Discovered and explicitly reported a browser rendering caveat**: `border-width` (unlike SVG `stroke-width`) gets snapped to whole device pixels by the browser's rasterizer at standard (1×) pixel density — confirmed via an isolated minimal-HTML test (`minitest.js`) showing `getComputedStyle(...).borderTopWidth` returns `"1px"` even when the source CSS says `1.5px`. The 1.5px value is still the technically-correct/matching declaration (and will render distinctly on HiDPI/Retina displays), but visually indistinguishable from 1px at 1× density in this test environment. This was surfaced to the user rather than silently worked around.
- Next request ("increase the line width... by 100%") doubled both border declarations from `1.5px` → `3px`, which **does** render as a visibly thicker rule even at 1× density (confirmed via screenshot) — this sidesteps the previous rounding issue by using a large-enough value that survives rounding either way.

### 6. Title text rename (eighth request)
- `<h2 class="panel-title fx-title">FX Circle</h2>` → `Fuxi circle`
- `<h2 class="panel-title kw-title">KW Square</h2>` → `King Wen square`
- Note: `.panel-title` already had (and still has) `text-transform: uppercase` in its CSS, unchanged and not requested to change — so these render as "FUXI CIRCLE" / "KING WEN SQUARE" on the page despite the mixed-case source text. Confirmed via screenshot this was consistent with the surrounding eyebrow/label styling and didn't break layout (KING WEN SQUARE is the longer string, checked for wrapping/overflow — none occurred).

### 7. FX hexagram hover-highlight (ninth request)
- New CSS rule: `.glyph.hex-hover .bar { stroke: var(--structure); }` (mirrors the existing `.glyph.active`/`.glyph.grouped` pattern).
- JS: inside the existing `document.querySelectorAll('.glyph').forEach(...)` loop (which already builds an invisible padded hit-rect per glyph half for click handling), added `mouseenter`/`mouseleave` listeners that look up **both** halves of the hexagram — `document.getElementById('glyph-' + n)` (inner/lower trigram) and `glyph-outer-' + n` (outer/upper trigram) — and toggle `.hex-hover` on **both together**, so hovering over either half highlights the whole 6-line hexagram, not just the half under the cursor. This was necessary because the two halves are separate sibling `<g>` elements in the SVG with no shared parent that a pure-CSS `:hover` selector could target.
- Verified via simulated `page.mouse.move()` to the center of `#glyph-1` and reading back `classList.contains('hex-hover')` + `getComputedStyle(...).stroke` on both halves — both turned to `rgb(162, 59, 46)` (`--structure` / `#A23B2E`) together. Screenshot confirms hexagram 1 (both trigram halves) rendering fully in the accent color on hover.

### 8. True visual-center title alignment (tenth, final request this session)
- Measured `fxTitleCenterX` vs. the FX circle's true geometric center (50% of the `<svg>` stage's rendered width, since `viewBox="0 0 1000 1000"` puts the ring center at exactly (500,500)) — found already aligned to within 0.008px, no change needed.
- Measured `kwTitleCenterX` vs. `.square`'s (the actual 8×8 hexagram grid, not the padded `.kw-square-frame` wrapper) true center — found off by **exactly −20px** (title 20px left of the square's real center). Root cause identified precisely: `.kw-square-frame { padding-left: 40px; }` (reserved gutter for the distance-marker overlay, added in an earlier session's KW-square-distance-markers work) shifts the square's visual content 20px right of the frame box's own center, while the title is centered on the *frame box*, not the square inside it.
- Fix: added `transform: translateX(20px);` to the existing `.kw-title { grid-column: 3; grid-row: 1; }` rule — a **title-only** correction. Deliberately did **not** touch `.kw-square-frame`'s padding or attempt to resize/recenter the frame itself, because that padding is load-bearing for other, unrelated JS (KW distance-bracket tick/overlay positioning computed elsewhere in the file against `kwFrame`'s bounding rect) and changing it risked cascading, hard-to-predict layout breakage elsewhere in this already-large file. Verified post-fix: both title-to-diagram center diffs are 0px (FX) and 0px (KW, was −20px).

## Full accumulated diff this session

`git diff --stat` at end of session: `diagrams/FX_circle_KW_square.html | 79 +++++++++++++++++++++++++++++++++------` (68 insertions, 11 deletions) — this is the **only** modified file; `git status --short` shows nothing else touched. Full `git diff` was captured and reviewed line-by-line as part of writing this handoff (see `<critical_context>` for the exact current state of the key CSS/JS blocks, reproduced there so a fresh session doesn't need to re-diff to know what's live).

</work_completed>

<work_remaining>

## Immediate — this session's own wrap-up (not yet done)

1. **Commit `diagrams/FX_circle_KW_square.html`** — all ten rounds of changes above are uncommitted. `git status --short` shows only this one file modified; nothing else in the working tree.
2. **Push to `origin/master`** — per the project's standing closing pattern (`feedback_push-reminder` memory), remind the user of this once committed. Nothing has been pushed this session; `origin/master` is still at `6f61fff` from before this session started.
3. This `whats-next.md` refresh itself (in progress as this document is written).

## Substantive follow-ups surfaced but not resolved this session

1. **`FX_KW_spine.html` does not exist.** The two new "FX SPINE"/"KW SPINE" links in `diagrams/FX_circle_KW_square.html` point to a placeholder filename (`FX_KW_spine.html#fx` / `#kw`) that was never confirmed with the user and has no corresponding page anywhere in the repo. This is explicitly a forward-reference to future work — the user said at the start of this thread "we're going to make a new connection to a new, **not yet ready**, 'FX_spine & KW_spine' page" — so this is expected/intentional dangling state, not a bug, but whoever builds that page next should either match the filename `FX_KW_spine.html` or update these two `href`s to whatever filename is actually chosen. Not yet added to `TO-DOS.md`.
2. **Minor open cosmetic question, not raised by the user, noticed only during this write-up:** the "spines box" border was doubled to `3px` per the most recent request, but the **outer `.unify-link` ("TABLE") box** still has `border: 1px solid var(--structure)` (its original, unchanged width) — this was never asked to be touched, so it's correctly left alone, but it now means the two stacked boxes ("spines box" above, "TABLE" box below) have visibly different border weights (3px vs 1px). If a future session gets a request like "make TABLE's border match the spines box" or vice versa, this is the relevant pair of rules (`.spine-link-group` border/divider vs. `.unify-link` border, both in the `<style>` block, both easy to find via the class names).

## From TO-DOS.md (verbatim list — see `<current_todos>` above; unchanged by this session)

1. XianTian trigram circle — annotate construction logic (binary/self-reversing vs mixed).
2. Trigram→hexagram concentric-ring diagram (inner 8 trigrams, outer 64 hexagrams).
3. Link the trigram circle + hexagram circle diagrams together.
4. Rebuild the hexagram Group Table from `data/spreadsheets/FX-01.ods` as canonical source.
5. FX/KW trigram circles paired diagram (needs verified King Wen trigram-position data, not assumed from memory).
6. Yin/yang group highlighting for trigrams (depends on item 1 being resolved first).
7. 3D trigram cubes "à la Z.D. Yung" — **needs user clarification** on the reference/convention before starting.
8. Central-Taiji digram/trigram linking page — **needs user clarification** on what "FX digrams" vs "KW digrams" means.
9. KW square distance-bracket markers ported to `diagrams/kw-square.html` (straight-line/tick version of the FX-circle-side arc distance markers in `FX_circle_KW_square.html`). **Note:** this item's wording talks about `diagrams/kw-square.html` specifically — a *different* file from `diagrams/FX_circle_KW_square.html`, which is the file all of this session's work happened in and which *already has* its own KW-square distance-bracket rendering (built in a prior session, per commit `7bc9dc9 Add KW square distance tokens/bracket and FX circle refinements`). Whether TO-DO item 9 is actually still outstanding (i.e., whether `diagrams/kw-square.html` — the standalone page — still lacks this feature) was **not checked or touched this session** and should be verified directly (open the file, check for `distance-overlay`/bracket-drawing code) before assuming it's stale, since `TO-DOS.md` has been shown twice now (this session and the prior one) to lag actual repo state.

</work_remaining>

<attempted_approaches>

## Things tried, reconsidered, or explicitly rejected mid-session

- **Naive `getBoundingClientRect()` for the distance-bracket bottom** — first attempt at aligning the "TABLE" box's bottom to the distance bracket used the outer `<svg>` element's own bounding box (fixed `height: 40px` in CSS). This was wrong by ~21px because the bracket's actual drawn content (a horizontal line + two tick-marks + a number label, all built in `renderPairDistanceBracket()`) is positioned near the *top* of that 40px box (`y = 8` in local SVG coordinates), not flush with the bottom. Caught by comparing the naive alignment result against a `getBBox()`-based measurement of the same element after the user reported the box was still "too low" after an ostensibly-correct-looking fix. **Lesson recorded for future work in this file:** any further alignment against `#pair-distance-fx`/`#pair-distance-kw` must use `svg.getBBox()` on the drawn content, never the outer `<svg>`'s own box model.
- **Trying to align FX-circle-center to KW-square-center by moving the KW square up (or the FX circle down) instead of accepting an enlarged KW gap** — considered but not pursued once the fixed-geometry math (`gap_KW = gap_FX + 78.19px`, derived from the two diagrams' differing rendered heights: ~636px visible circle vs. 480px square grid) showed there is no configuration of the two independent `margin-top` values that keeps *both* gaps small while also keeping centers aligned and titles on a shared row — one gap must always end up substantially larger than the other. Resolved by explicitly telling the user the trade-off rather than silently picking one, and proceeding once they confirmed satisfaction ("that looks good").
- **Resizing `.kw-square-frame`'s `padding-left`/adding symmetric `padding-right`** — considered as an alternative fix for the final title-centering request (item 8 above), instead of the `translateX(20px)` actually used. Rejected because the frame's asymmetric padding is read by other, unrelated JS in the file (KW distance-bracket overlay positioning, computed against `kwFrame.getBoundingClientRect()`) and changing the box model there risked breaking that feature in ways that would require re-testing the entire distance-bracket interaction, for a fix that a single-property, title-only `transform: translateX()` achieves with zero blast radius.
- **`npx playwright`** — first attempt at getting a headless browser for measurement used `npx --yes playwright`, which resolved/ran but `require('playwright')` inside a plain Node script failed (`MODULE_NOT_FOUND`) since `npx` on its own doesn't install the package into a resolvable `node_modules` for a separately-invoked script. Switched to `npm install playwright-core` in a scratchpad subdirectory plus the system's pre-installed `/usr/bin/chromium-browser` (found via `which chromium chromium-browser google-chrome`) passed explicitly as `executablePath`, which worked reliably for the rest of the session.

</attempted_approaches>

<critical_context>

## Reference unit established this session: "one hexagram height" = 32px

Taken directly from this file's own `.hex-glyph` markup (`viewBox="0 0 30 32" width="30" height="32"`, used for the KW-square cell hexagrams and the pair-display-box hexagrams). Used repeatedly, per explicit user instructions phrased in these terms ("150% the height of a hexagram", "lower... by about the height of a hexagram", "raise the box by 40% the height of the box" [note: this last one is 40% of the *box's own* height, not the hexagram unit — don't conflate the two]). If a future session gets another "N% of a hexagram" instruction in this file, 32px (or 1.5× = 48px, as already used once) is the correct base value, not something to re-derive from scratch.

## Current, live state of the key CSS rules in `diagrams/FX_circle_KW_square.html` (as of end of session)

```css
.panel-title { font-family: var(--font-mono); font-size: 1.56rem; letter-spacing: 0.12em; text-transform: uppercase; color: var(--structure); margin: 0; font-weight: 400; justify-self: center; }
.fx-title { grid-column: 1; grid-row: 1; }
.kw-title { grid-column: 3; grid-row: 1; transform: translateX(20px); }
.diagram { justify-self: center; align-self: center; }
.fx-diagram { grid-column: 1; grid-row: 2; pointer-events: none; margin-top: -44.6px; }
.kw-diagram { grid-column: 3; grid-row: 2; align-self: start; margin-top: 74.2px; }
...
.unify-link { display: none; position: absolute; transform: translate(-50%, -50%); font-family: var(--font-mono); font-size: 0.78rem; letter-spacing: 0.08em; color: var(--structure); border: 1px solid var(--structure); border-radius: 6px; padding: 8px 14px; text-decoration: none; white-space: nowrap; }
.unify-link:hover { background: var(--structure); color: var(--paper); }
.unify-link.active { display: inline-block; }

.spine-link-group { display: none; position: absolute; transform: translate(-50%, -50%); flex-direction: column; font-family: var(--font-mono); font-size: 0.78rem; letter-spacing: 0.08em; border: 3px solid var(--structure); border-radius: 6px; overflow: hidden; }
.spine-link-group.active { display: flex; }
.spine-link-group a { color: var(--structure); padding: 8px 14px; text-decoration: none; text-align: center; white-space: nowrap; }
.spine-link-group a:not(:last-child) { border-bottom: 3px solid var(--structure); }
.spine-link-group a:hover { background: var(--structure); color: var(--paper); }
...
.glyph.hex-hover .bar { stroke: var(--structure); }
```

## Current, live HTML for the link boxes

```html
<a class="unify-link" id="unify-link" href="group-table.html" target="groups-table">TABLE</a>
<div class="spine-link-group" id="spine-link-group">
<a id="spine-link-fx" href="FX_KW_spine.html#fx" target="fx-kw-spine">FX SPINE</a>
<a id="spine-link-kw" href="FX_KW_spine.html#kw" target="fx-kw-spine">KW SPINE</a>
</div>
```

## Current, live `positionUnifyLink()` function (drives both the "TABLE" box and the "spines box")

```js
function positionUnifyLink() {
  var unifyLink = document.getElementById('unify-link');
  var spineLinkGroup = document.getElementById('spine-link-group');
  var panelsRect = document.querySelector('.panels').getBoundingClientRect();
  var fxDisplay = document.getElementById('pair-display-fx');
  var kwDisplay = document.getElementById('pair-display-kw');
  var fx = fxDisplay.getBoundingClientRect();
  var kw = kwDisplay.getBoundingClientRect();
  var centerX = (fx.right + kw.left) / 2 - panelsRect.left;

  var fxGlyph = fxDisplay.querySelector('.pd-glyph').getBoundingClientRect();
  var kwGlyph = kwDisplay.querySelector('.pd-glyph').getBoundingClientRect();
  var glyphCenterY = (((fxGlyph.top + fxGlyph.bottom) / 2) + ((kwGlyph.top + kwGlyph.bottom) / 2)) / 2 - panelsRect.top;
  spineLinkGroup.style.left = centerX + 'px';
  spineLinkGroup.style.top = glyphCenterY + 'px';

  function bracketBottom(svgNode) {
    var bb = svgNode.getBBox();
    return svgNode.getBoundingClientRect().top + bb.y + bb.height;
  }
  var fxDistance = pairDistanceFxSvg.childNodes.length ? bracketBottom(pairDistanceFxSvg) : pairDistanceFxSvg.getBoundingClientRect().bottom;
  var kwDistance = pairDistanceKwSvg.childNodes.length ? bracketBottom(pairDistanceKwSvg) : pairDistanceKwSvg.getBoundingClientRect().bottom;
  var distanceBottom = ((fxDistance + kwDistance) / 2) - panelsRect.top;
  var unifyHeight = unifyLink.getBoundingClientRect().height;
  unifyLink.style.left = centerX + 'px';
  unifyLink.style.top = (distanceBottom - unifyHeight / 2 - unifyHeight * 0.4) + 'px';
}
```

Note the `pairDistanceFxSvg`/`pairDistanceKwSvg` variables referenced here are pre-existing module-level `var`s (`document.getElementById('pair-distance-fx'/'pair-distance-kw')`) defined earlier in the same `<script>` block, not new to this session.

## Current, live hover-handling addition inside the `.glyph` click-setup loop

```js
document.querySelectorAll('.glyph').forEach(function (glyphEl) {
  var m = glyphEl.id.match(/^glyph-(?:outer-)?(\d+)$/);
  if (!m) return;
  var n = parseInt(m[1], 10);
  var bbox = glyphEl.getBBox();
  var pad = 6;
  var hit = svgEl('rect', { x: (bbox.x - pad).toFixed(2), y: (bbox.y - pad).toFixed(2), width: (bbox.width + pad * 2).toFixed(2), height: (bbox.height + pad * 2).toFixed(2), fill: 'transparent', 'pointer-events': 'all' });
  glyphEl.insertBefore(hit, glyphEl.firstChild);
  glyphEl.addEventListener('click', function () { toggleGroupFor(n); });
  var inner = document.getElementById('glyph-' + n);
  var outer = document.getElementById('glyph-outer-' + n);
  glyphEl.addEventListener('mouseenter', function () {
    if (inner) inner.classList.add('hex-hover');
    if (outer) outer.classList.add('hex-hover');
  });
  glyphEl.addEventListener('mouseleave', function () {
    if (inner) inner.classList.remove('hex-hover');
    if (outer) outer.classList.remove('hex-hover');
  });
});
```

## Verification methodology used throughout (reusable for future sessions on this file)

- Scratchpad dir this session: `/tmp/claude-1000/-home-greg-pCloudDrive-YIJING-Yijing-Pathways/30dab904-284f-44ea-bb39-9bdfac044e68/scratchpad/pw/` — **session-scoped, will not exist in a fresh session.** Contains `package.json`/`node_modules` for `playwright-core` and ~18 numbered `measure*.js` throwaway scripts plus `solve.js`/`minitest.js`/`shot.js`.
- Reusable pattern for a fresh session: `npm install playwright-core` in a new scratchpad dir, then `chromium.launch({ executablePath: '/usr/bin/chromium-browser', args: ['--no-sandbox'] })` (the system Chromium at this path was confirmed present and working; `/snap/bin/chromium` also exists as an alternative). Load the file via `file://` URL, `page.click('#glyph-1')` (or any `[data-num]`/`.cell[data-hex]`) to trigger `showGroup()` and populate the pair-display/distance-bracket/link-box elements (most of the elements this session's work centered on are `display:none` until a group is selected), then measure with `getBoundingClientRect()`/`getBBox()` as needed, and `page.screenshot({ path, fullPage: true })` for visual confirmation.
- This matches (and should continue to follow) the project's `feedback_verification-standard` persistent memory: structural/visual claims in this project need computational proof via actual rendering, not eyeballed code review.

## Persistent-memory context relevant to this project (carried forward, not re-derived this session)

- `feedback_verification-standard`: structural claims need exhaustive computational proof, not eyeballing — this was the dominant methodology all session (see above).
- `feedback_handoff-staleness-check`: `whats-next.md` can lag actual repo state — directly confirmed again at the very start of this session (prior handoff was 5 commits stale).
- `feedback_whats-next-leads-with-todos`: lead first response with the to-do list when reading `whats-next.md` at session start — followed.
- `project_github-setup`: public repo, GitHub Pages live at `gregrosser.github.io/Yijing-Pathways`, pushes to `master` auto-deploy — relevant once this session's changes are pushed; the live site's `FX_circle_KW_square.html` page will pick up all ten rounds of changes.
- `feedback_push-reminder`: remind the user to consider `git push` to master before ending a session — applies now, once a commit is made (see `<work_remaining>`).
- `project_spine-page-css-gotcha`: same-shape panel pairs need explicit page-width + custom gap, not auto-sizing — directly relevant/consistent with this session's repeated discovery that the FX-circle/KW-square pairing needed explicit, independently-computed `margin-top` values rather than relying on shared/auto grid alignment (`align-items`/`align-self: center`) to make two differently-sized panels line up correctly.
- `project_asana-removed`, `reference_pcloud-backups`, `reference_obsidian-vault`: not touched or relevant this session.

</critical_context>

<current_state>

## Git — one file's worth of ten rounds of changes, fully uncommitted

```
$ git status --short
 M diagrams/FX_circle_KW_square.html
$ git diff --stat
 diagrams/FX_circle_KW_square.html | 79 +++++++++++++++++++++++++++++++++------
 1 file changed, 68 insertions(+), 11 deletions(-)
```

`TO-DOS.md` is **unmodified** this session (confirmed via `git status` showing it clean) — the `<current_todos>` block above is simply its current, accurate, unchanged contents.

`origin/master` is still at `6f61fff` ("Add matching distance brackets under each pair-display box") — nothing pushed this session.

## Deliverable status

All ten rounds of UI-refinement requests against `diagrams/FX_circle_KW_square.html` are **complete and individually verified** (computationally, per-request, via the Playwright harness) but **not yet committed or pushed**. No other files were touched. No task from this session is left half-finished — each request was carried through to a verified, screenshotted end state before the next request began.

## Immediate next step

1. Confirm with the user whether to commit `diagrams/FX_circle_KW_square.html` now (likely yes, given the session ended on "refresh the to-do list", i.e., a natural wrap-up point).
2. Commit with a message describing the cumulative FX_circle_KW_square.html UI-refinement work (title sizing/centering, circle/square vertical alignment, new spine-navigation link box, hover-highlight, border-width matching) — probably as one commit given it's all one coherent session of iterative polish on one file, matching this project's usual pattern of one commit per logical unit of work.
3. Push to `origin/master` — remind the user per `feedback_push-reminder`.
4. Separately flag to the user (not yet done): the two new spine-navigation links point to a placeholder, non-existent `FX_KW_spine.html` — worth confirming the eventual filename before that page is built, and/or adding a TO-DOS.md entry for building it if one doesn't already exist (it currently does not — verified via `grep`-equivalent read of the full current `TO-DOS.md`, reproduced verbatim in `<current_todos>` above).

</current_state>
