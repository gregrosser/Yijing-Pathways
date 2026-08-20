<reading_instructions>
Whoever reads this document — a fresh Claude instance resuming this work, at the start of a new session — must lead their first response to the user with the contents of <current_todos> below, before summarizing <original_task>, <work_completed>, or anything else in this document.
</reading_instructions>

<current_todos>
# TO-DOS

## Footer nav links don't reuse an already-open tab in Firefox - 2026-08-20 14:11

- **Named-target footer links (`diagrams/FX_KW_spine.html`) aren't reusing an already-open destination tab in the user's actual Firefox browser, even though the tab was itself opened via the same link.** The three footer buttons — "Yijing Pathways", "FX circle / KW square", "Groups table" — each got a `target="..."` attribute this session (`target="yijing-pathways"`, `target="fx-circle-kw-square"`, `target="groups-table"`) specifically so that clicking one when its destination page is already open in another tab would return to/focus that tab instead of opening a new one, matching the pre-existing convention already used elsewhere in this project (`FX_circle_KW_square.html`'s own `target="fx-kw-spine"` and `target="groups-table"` links). **Problem:** verified working correctly in headless Chromium (`context.pages().length` stayed at 2 after clicking the same link twice — see the session's `test_targets.js` in a now-gone scratchpad, easy to recreate) — but the user, testing live in Firefox, reported the link still opens a brand-new tab on a second click, even after explicitly confirming (via the session's `AskUserQuestion`) that the already-open tab *was* itself opened by clicking that same link earlier — which was expected to be the one case where reuse should reliably work. The user had to leave mid-diagnosis, so this is unconfirmed/unresolved, not yet root-caused. **Not touched in the two most recent sessions** (this handoff's session, or the one before it) — still the top open item. **Files:** `diagrams/FX_KW_spine.html` (the three footer links, this session's new `target=` attributes); `diagrams/FX_circle_KW_square.html` (pre-existing `target="fx-kw-spine"`/`target="groups-table"` links on `spine-link-fx`/`spine-link-kw`/`unify-link` — worth checking whether *this* older pre-existing target-reuse behavior also fails for the user in real Firefox, or whether it's specific to the newly-added links, since that would narrow down whether this is a Firefox quirk with named targets in general vs. something specific to this session's change). **Solution:** not yet found — next session should first try to get a precise, minimal repro (e.g. a two-link toy HTML file) to isolate whether this is a Firefox-specific bug/setting around named-window-target matching (there's a real, documented Firefox preference `browser.link.open_newwindow` and related tab-vs-window handling that can affect this), whether it's specific to `file://` origins (already established this session that Firefox isolates each `file://` URL as its own origin, which broke other cross-tab approaches — worth checking if that isolation also affects named-target matching, not just storage/messaging APIs), or whether the *existing* `fx-kw-spine`/`groups-table` targets on `FX_circle_KW_square.html` have the exact same problem and it's simply never been noticed before. Ask the user to check Firefox's `about:preferences#general` tab-opening settings, and/or test target-reuse with a trivial two-page reproduction outside this project's actual files to isolate the variable.

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
This session opened with the user asking to read `whats-next.md`, a handoff document from a prior session. That prior handoff described `diagrams/FX_KW_spine.html` and `diagrams/FX_circle_KW_square.html` as having substantial uncommitted work (display boxes, click-selection, footer nav, distance brackets, a Firefox stroke-rendering fix) plus an unresolved Firefox tab-reuse bug as the top TO-DOS.md item. On resuming, this session's first action was to summarize that handoff for the user and ask whether to continue diagnosing the Firefox tab-reuse bug or do something else first.

The user did not continue the Firefox diagnosis. Instead, all substantive work this session was a sequence of independent, user-directed edit requests, each building on the last:

1. Edit `diagrams/FX_KW_spine.html`: remove the spine-side "distance" brackets altogether, keep the display-box "distance" brackets as they were.
2. Increase the display-box distance font size by 100%.
3. (User: "oops, too much") Reduce the distance font by 50%.
4. (User: "oops, too much") Increase the distance font by 50%.
5. Edit `diagrams/group-table.html`: add KW "distance" values next to the KW groups, positioned so both new distance columns land in the central gap between the KW-left-nums and KW-right-nums (left-side/line1==line6 groups: distance to the right of KW-nums; right-side/line1≠line6 groups: distance to the left of KW-nums).
6. Put the new KW distance values in square boxes (vs. the existing circular FX distance badges).
7. Change both FX and KW distance badges' default color to the page's normal ink/black color, only switching to the highlight color when a group is selected (hovered or clicked).
8. End of session: "that's it for today. clean up the to-do list and then refresh the whats-next." — this document is that refresh; TO-DOS.md was reviewed but needed no changes (see `<work_completed>` below for why).

No commit or push has been requested or made at any point in this session.
</original_task>

<work_completed>

## 0. Discovered the previous handoff was stale (confirms `feedback_handoff-staleness-check` memory)

Before any edits, git state showed only `diagrams/FX_KW_spine.html` and `diagrams/group-table.html` as modified — **not** `diagrams/FX_circle_KW_square.html` or `TO-DOS.md`, which the prior whats-next.md had described as uncommitted. Checking `git log`/`git reflog` showed commit `d62f08c` ("Add hexagram display boxes, click-to-select, and button footer nav to FX/KW spine page"), timestamped today (2026-08-20 14:16:34), already contains everything that prior handoff described as pending: the display boxes, click-selection, footer nav, `?fx=` propagation, and the Firefox-safe filled-rect distance brackets. **In other words, between that handoff being written and this session starting, the described work was already committed** (evidently by the user or another session in between). This session's starting git status is therefore the true baseline — only today's own edits (items 1–7 above) are uncommitted.

## 1. Removed the spine-side distance brackets from `diagrams/FX_KW_spine.html`

Deleted entirely, leaving the under-box (`.hd-distance-*`) brackets untouched:
- CSS: `.distance-overlay`, `.distance-bracket-line`, `.distance-tick`, `.distance-label-bg`, `.distance-label-text` rules (were around original lines 98–108; the `.hd-distance-*` equivalents for the under-box brackets were left in place).
- HTML: the two `<svg id="fx-distance-overlay" class="distance-overlay"></svg>` / `<svg id="kw-distance-overlay" class="distance-overlay"></svg>` elements (were inside `.fx-spine-frame`/`.kw-spine-frame`, just before each panel's `.name-tag` div).
- JS: the entire `drawDistanceBracket(overlay, frame, svg, prefix, selectedSet, distance, shape, lineXFn, tickXFn)` function (had computed tick/label geometry keyed to the spine SVGs' own coordinate space, using `REFERENCE_SVG_HEIGHT`/`DISTANCE_LABEL_RADIUS_REF`/`DISTANCE_LABEL_FONT_SIZE_REF`/`GUTTER_FRACTION` — all four of those reference constants were also removed since nothing else used them), its two call sites inside `update()` (which had passed `GUTTER_FRACTION`-based `lineXFn`/`tickXFn` closures for the FX/KW gutter geometry), and the `fxOverlay`/`kwOverlay` `document.getElementById(...)` variable declarations. `fxFrame`/`kwFrame` were **kept** — they're still used by `positionHexDisplays()` for unrelated layout math.
- Verified via `node --check` on the extracted `<script>` block that the JS still parses cleanly after all removals, and via `grep` that no reference to `distance-overlay`, `drawDistanceBracket`, `fxOverlay`/`kwOverlay`, or the four removed reference constants remains anywhere in the file.
- **Not visually verified in a real browser** — Playwright's Chromium isn't installed in this environment (`Error: async initializeServer: Chromium distribution 'chrome' is not found at /opt/google/chrome/chrome`), and per this project's established Firefox-vs-Chromium rendering gotchas (see prior session's `<critical_context>`, still true), a live look in the user's actual Firefox is the only real check anyway. The user has since used the page (making further requests against it) without reporting any visual problem from this removal.

## 2–4. Display-box distance font-size back-and-forth (net result: 24px → 36px)

All edits were to a single line, `renderHdDistanceBracket()`'s local var declaration (currently around line 587 post-edit-1's line-number shifts):
- Start: `fontPx = 24` (the pre-existing value, inherited unchanged from the prior session's under-box bracket work).
- Step 2 (+100%): `fontPx = 48`. The label circle/rect radius (`half = 15/16 * fontPx`) and the SVG's own `height` attribute both derive from `fontPx`, so they scaled proportionally with no other code changes needed.
- Step 3 (user: "oops, too much" — reduce by 50%): `fontPx = 24` (50% of 48 — back to the original value, though framed by the user as a correction rather than "revert").
- Step 4 (user: "oops, too much" — increase by 50%): `fontPx = 36` (150% of 24). **This is the final value left in the file.**

No other geometry in `renderHdDistanceBracket()` needed adjustment across these changes — `barY`, `tickTopY`, `strokeW` are independent constants, and the SVG's `height` attribute (`barY + half + 4`) auto-adjusts each time since `half` is a function of `fontPx`.

## 5. Added KW-distance badges to `diagrams/group-table.html` (all 20 group cells)

**Positioning mechanism (the key design insight):** each `.cell` is a flex container. Left-column cells (`Axis — FX(31,32)`, i.e. line1==line6 groups) use normal `flex-direction: row`; right-column cells (`Axis — FX(33,34)`, line1≠line6) use `.cell.right { flex-direction: row-reverse; }`. Each cell's existing DOM order is `[dist-badge (FX), set-label (FX), members, kw-label (KW)]`. Appending the new KW-distance badge as the cell's **last DOM child** (i.e., right after the `kw-label` div, before the cell's closing `</div>`) is the single insertion rule that produces the correct mirrored visual result on both sides simultaneously:
  - Left cells (normal row): last DOM child = rightmost visually → badge lands to the **right** of KW-nums.
  - Right cells (row-reverse): last DOM child = **leftmost** visually → badge lands to the **left** of KW-nums.
  - Since each column's `kw-label` already sits adjacent to the table's central gap (by the same DOM-order-plus-flex-direction logic, pre-existing), both new badges land immediately next to each other in that central gap, exactly as requested.

**Data used:** the KW-distance value for each group is computed with the exact same formula as `kwGroupDistance()`/`kwPairIndexRange()` in `diagrams/FX_KW_spine.html` (sort the group's KW numbers ascending; for a quartet take `a = kw[0]`, `b = kw[2]`; for a pair, `a = b = kw[0]`; distance = `(b+1)/2 - (a+1)/2 + 1`), applied directly to the KW numbers already present in each cell's `kw-label` (no need to go via FX numbers/`FX_TO_KW`, since the KW numbers were already in the DOM). Computed and inserted programmatically (Python script over the file's HTML, not hand-typed), verified all 20 results came out as exact integers (a strong correctness check, since the formula only produces integers for a valid pairing) and cross-checked count (20 cells → 20 badges, no duplicates, no misses).

**Markup added per cell:** `<div class="dist-badge kw-dist-badge" title="KW dist">N</div>` — reuses the existing `.dist-badge` circular-badge visual base class plus a new `.kw-dist-badge` modifier class for position-specific overrides.

**Mistake made and corrected mid-edit:** the first attempted regex substitution only matched `class="kw-label mono"` exactly, missing the 8 pair-type cells whose kw-label carries an extra class (`class="kw-label mono pair-num"`). Running it anyway produced correct results for the 12 quartet-type cells but silently skipped the 8 pair-type ones. Re-running a *second*, broader-matching pass on top of that (intending to "fill the gap") instead **re-matched and duplicated** the 12 already-done quartet cells (each ended up with two identical badges) while still handling the 8 pair cells correctly, since the second pass's pattern didn't check for a pre-existing badge before inserting. **Recovered via `git checkout -- diagrams/group-table.html`** (safe, since `git diff --stat` before that point still showed only additions, nothing else in the file had been touched, and the original was intact in the working tree's last commit) and re-ran a single corrected pass (pattern: `class="kw-label mono( pair-num)?"`) that handled both cell types in one pass. Verified afterward: exactly 20 `.kw-dist-badge` elements in the final file, one per cell, no duplicates.

## 6. Made KW-distance badges square

Added `border-radius: 0` to the `.kw-dist-badge` CSS rule (`diagrams/group-table.html`), so KW badges render as squares against the FX `.dist-badge`'s inherited `border-radius: 50%` (circle) — matching this project's existing circle-for-FX/square-for-KW convention used elsewhere (`FX_circle_KW_square.html`'s `kw-distance-label-bg` is a plain `<rect>` with no rounding, `FX_KW_spine.html`'s `renderHdDistanceBracket(..., shape)` takes `'circle'`/`'square'` as an explicit parameter).

## 7. Distance badges: default ink color, highlight color only when a group is active

Changed `.dist-badge`'s base `border` and `color` from `var(--structure)` (the page's accent/highlight color, a rust-red `#A23B2E` in light mode) to `var(--ink)` (the page's normal body-text color). Added a new rule, `.cell:has(.num.hl) .dist-badge { border-color: var(--structure); color: var(--structure); }`, which re-applies the highlight color to **both** badges in a cell (the FX `.dist-badge` and the KW `.kw-dist-badge`, since the latter also carries the `.dist-badge` class) whenever that cell contains a `.num.hl` element. `.num.hl` is the pre-existing class this page's script already toggles on individual FX/KW number spans via `setHighlight(fx, on)` — used identically for both hover-preview (`mouseenter`/`mouseleave` in `wire()`) and click-based selection (`toggleSelect()`), so this new rule automatically covers "a group is selected" without any JS changes, by design consistency with how every other highlightable element on this page already works (hover and click-select share the same visual treatment throughout). No JS was touched for this change — purely a CSS addition plus base-color edit.

## Session close: TO-DOS.md reviewed, no changes needed

The user asked to "clean up the to-do list" before this handoff refresh. Reviewed `TO-DOS.md` in full: **none of today's session's work items (spine-bracket removal, font sizing, group-table KW-distance badges) were themselves TO-DOS.md entries** — they were all ad hoc requests from the user, not items being checked off the list. None of the 4 TO-DOS.md sections (Firefox tab-reuse bug, XianTian circle diagrams, trigram circles/cubes/Taiji page, KW square distance markers) were touched or resolved this session, so the file needed no edits. It is reproduced verbatim, unchanged, in `<current_todos>` above.

</work_completed>

<work_remaining>

## Immediate — nothing outstanding from today's specific requests

Every explicit request this session (items 1–7 in `<original_task>`) was completed and left in a working state as far as static verification allows. The one caveat: **none of today's `diagrams/FX_KW_spine.html` or `diagrams/group-table.html` changes have been visually confirmed in the user's real Firefox** — this environment has no working Chromium for Playwright either (`chrome` binary missing), so verification this session was limited to `node --check` syntax validation, `grep`-based structural checks, and (for the group-table KW-distance formula) a Python-side integer-consistency check across all 20 groups. Given this project's well-established history of Chromium-vs-Firefox rendering discrepancies (see `<critical_context>` below), a live look in Firefox is worth doing early next session if anything looks off, especially:
- The `:has()` CSS selector used in item 7's highlight rule (`.cell:has(.num.hl) .dist-badge`) — modern and widely supported, but worth confirming it actually fires as expected on hover/click in the user's real browser, not just structurally present in the CSS.
- The removed spine-side brackets in `FX_KW_spine.html` — confirm no dangling visual artifact or layout shift resulted from their removal.

## From `TO-DOS.md` (verbatim in `<current_todos>` above — unchanged this session, still the complete, current, ordered list)

1. **[Top priority, unresolved for two sessions running]** Firefox tab-reuse bug on the footer nav links (`diagrams/FX_KW_spine.html`'s `target="..."` attributes) — root cause still unknown. See the full entry in `<current_todos>` for the specific next diagnostic steps already identified (check whether `FX_circle_KW_square.html`'s older pre-existing targets have the same problem; check Firefox's `browser.link.open_newwindow` and `about:preferences#general`; build a minimal two-page repro outside this project).
2. XianTian trigram circle — annotate construction logic (binary/self-reversing vs. mixed).
3. Trigram→hexagram concentric-ring diagram.
4. Link the trigram circle + hexagram circle diagrams together.
5. Rebuild the hexagram Group Table from `data/spreadsheets/FX-01.ods` (note: today's group-table.html edits were additive UI changes to the *existing* table, not a rebuild from the spreadsheet — this TO-DO item is about a more fundamental data-source rework and remains fully open).
6. FX/KW trigram circles paired diagram (needs verified King Wen trigram-position data).
7. Yin/yang group highlighting for trigrams (depends on item 2).
8. 3D trigram cubes "à la Z.D. Yung" — needs user clarification on the reference.
9. Central-Taiji digram/trigram linking page — needs user clarification on "digrams."
10. KW square distance-bracket markers on standalone `diagrams/kw-square.html` (a *different* file from `group-table.html` — today's work did not touch this) — status unverified, inherited unchanged from before.

</work_remaining>

<attempted_approaches>

- **Group-table KW-distance-badge insertion, first regex pass** — pattern `class="kw-label mono"` (exact match) missed the 8 pair-type cells (`class="kw-label mono pair-num"`), silently inserting badges for only 12 of 20 cells. **Lesson: when a CSS class attribute can carry extra modifier classes (`pair-num` here), match defensively for that (`( pair-num)?` or similar) rather than assuming a fixed class string** — this file's own earlier `.set-label.pair-num, .kw-label.pair-num { ... }` CSS rule was direct evidence such a modifier existed, and should have been checked before writing the first regex.
- **Second regex pass to "fill the gap" from the first pass's incomplete result** — matched *all* 20 kw-label divs (correctly, this time, with the broadened pattern) but didn't check whether a `.kw-dist-badge` already followed a given kw-label before inserting, so it **duplicated** the 12 cells the first pass had already handled correctly. Recovered cleanly via `git checkout -- diagrams/group-table.html` (verified first that `git diff --stat` showed only additions and no other file damage) and re-ran a single, correctly-scoped pass instead of trying to patch the duplicates in place. **Lesson: prefer reverting to a known-clean baseline and re-running one correct pass over trying to layer a second corrective pass on top of a partially-wrong one**, especially for scripted/regex-driven bulk edits where "did it match the right set, exactly once each" is easy to get subtly wrong.
- No other dead ends this session — the remaining edits (spine-bracket removal, font-size changes, square-badge CSS, ink/highlight color rule) were each single, correctly-scoped changes on the first attempt.

</attempted_approaches>

<critical_context>

## This session's key structural/design decisions (for anyone editing these files next)

- **`diagrams/FX_KW_spine.html` no longer has *any* spine-side distance-bracket overlay.** The only remaining distance readout on that page is the under-box bracket (`renderHdDistanceBracket()`, `.hd-distance-svg`/`.hd-distance-bracket-line`/`.hd-distance-tick`/`.hd-distance-label-bg`/`.hd-distance-label-text`), which was already Firefox-safe (filled rects, not stroked lines — a fix from a prior session) and unaffected by today's removal. If a future request references "the distance bracket" on this page ambiguously, it now means *only* the under-box one — there is no longer a second, spine-side one to disambiguate against.
- **`renderHdDistanceBracket()`'s `fontPx` is currently `36`** (see `<work_completed>` §2–4 for the back-and-forth that arrived here). If asked to adjust this again, note the label's circle/square radius and the containing SVG's rendered height both derive from this single value (`half = 15/16 * fontPx`; SVG `height = barY + half + 4`), so changing it alone keeps everything proportioned — no other constant needs touching.
- **`diagrams/group-table.html`'s distance-badge insertion point (last DOM child of each `.cell`) is deliberately exploiting the existing `flex-direction: row` / `row-reverse` split** between left- and right-column cells to get mirrored positioning "for free" from one insertion rule. If a future change reorders any cell's DOM children (e.g., inserting something else after `kw-label`), this positioning breaks silently (the badge would just end up in a different visual slot, not throw an error) — worth re-checking visually if that ever happens.
- **The new `.cell:has(.num.hl) .dist-badge` highlight rule relies on `:has()`** — this project's other pages don't currently use `:has()` anywhere else (checked: no other `:has(` in the codebase as of this session), so this is a new pattern for this codebase. It should work in any reasonably current browser (including the user's confirmed Firefox 154 from prior-session `navigator.userAgent` diagnostics — Firefox has supported `:has()` since v121), but is worth flagging as the first use of this selector here in case it ever needs a fallback.
- **`diagrams/group-table.html`'s KW-distance values were derived, not looked up from any external source** — computed directly from the KW numbers already embedded in each cell's `kw-label` div using the identical formula already implemented in `diagrams/FX_KW_spine.html`'s `kwGroupDistance()`. If the two files' KW-distance values are ever compared side-by-side for the same groups, they should match exactly (both derive from the same `FX_TO_KW` mapping and the same pairing formula) — this would be a good sanity check if either file is modified again later and a discrepancy would flag a bug.

## Carried forward from the prior session (still true, not re-verified this session but no evidence of change)

- **The user's real browser is Firefox** (`Mozilla/5.0 (X11; Linux x86_64; rv:154.0) Gecko/20100101 Firefox/154.0`), confirmed via a console dump in a prior session — not Chromium-based despite some earlier, since-corrected guessing based on screenshot chrome styling.
- **Firefox implements page zoom by shrinking `devicePixelRatio`**, not widening the layout viewport — Chromium-based automated testing (including this environment's, when it has a working Chromium) does not faithfully reproduce real Firefox zoom behavior. The user's typical viewing zoom is ~20%, confirmed `devicePixelRatio: 0.2` in a prior session.
- **Firefox treats every distinct `file://` URL as its own isolated origin** — rules out `localStorage`/`BroadcastChannel`-based cross-tab-communication workarounds for this project's pages, and is a live open question for the still-unresolved Firefox tab-reuse bug (does this isolation extend to named-`target=` window matching, not just storage APIs? — not yet determined).
- **Firefox renders thin *stroked* SVG lines inside an absolutely-positioned nested `<svg>` overlay unreliably at extreme `devicePixelRatio`** (established via a prior session's multi-round bug hunt on the now-removed spine-side bracket) — the general lesson (prefer filled shapes over stroked lines for any new SVG overlay work on this project's pages, especially anything meant to render correctly at the user's extreme zoom) remains valid and should still be applied to any *new* SVG drawing code, even though the specific bracket that prompted the discovery no longer exists.
- **This environment currently has no working browser for live/automated verification.** Playwright's Chromium is not installed (`chrome` binary missing at `/opt/google/chrome/chrome`, and `npx playwright install chrome` was not run this session since it wasn't clear that was wanted without asking first). This is a capability gap, not a code problem — worth flagging to the user or fixing (`npx playwright install chrome`) if visual/interactive verification becomes necessary and blocking for a future task.

## Relevant persistent memory (see `/home/greg/.claude/projects/-home-greg-pCloudDrive-YIJING-Yijing-Pathways/memory/`)

`feedback_handoff-staleness-check` (directly relevant and reconfirmed this session — see `<work_completed>` §0), `feedback_verification-standard`, `feedback_whats-next-leads-with-todos` (followed), `feedback_push-reminder` (applies — no commit/push made or requested this session despite 7 rounds of verified changes across 2 files), `project_github-setup`, `project_spine-page-css-gotcha`, `project_asana-removed`, `reference_pcloud-backups`, `reference_obsidian-vault`, `user_extreme-zoom-out-viewing` (relevant background for why font-size/legibility requests like items 2–4 come up at all on this project's diagram pages, though not directly invoked this session).

</critical_context>

<current_state>

## Git status

```
$ git status --short
 M diagrams/FX_KW_spine.html
 M diagrams/group-table.html
```

`git diff --stat`:
```
 diagrams/FX_KW_spine.html | 120 +---------------------------------------------
 diagrams/group-table.html |  38 ++++++++++++++-
 2 files changed, 37 insertions(+), 121 deletions(-)
```

`origin/master` is at `d62f08c` (which, per `<work_completed>` §0, already includes everything the *previous* handoff described as pending — this session's own two modified files are the only genuinely new uncommitted work). **No commit or push has been made or requested this session.**

## Deliverable status

- `diagrams/FX_KW_spine.html`: spine-side distance brackets fully removed (CSS/HTML/JS, all three verified absent via grep), display-box distance font resized to a final `fontPx = 36`. Structurally verified (`node --check` on extracted JS); not visually verified in any browser this session (no working Chromium in this environment; Firefox verification would need the user).
- `diagrams/group-table.html`: KW-distance badges added to all 20 group cells (verified count and formula correctness programmatically), styled square (`border-radius: 0`), and both FX/KW badges now default to ink color with highlight-color-on-`.hl` via a new `:has()` CSS rule. Not visually verified in any browser this session, same caveat as above.
- `TO-DOS.md`: reviewed, unchanged — no session items were TO-DOS.md entries, nothing to remove. Reproduced verbatim in `<current_todos>` above.
- `whats-next.md` (this file): this refresh, written at explicit user request ("that's it for today. clean up the to-do list and then refresh the whats-next.") to close out the session.

## Immediate next step for whoever resumes

1. Greet/resume with the user, lead with `<current_todos>` as instructed.
2. Per `feedback_push-reminder`, consider reminding the user that today's two-file diff (`FX_KW_spine.html`, `group-table.html`) is still uncommitted — but only *remind*, don't commit unprompted, consistent with this project's established pattern of the user driving every commit explicitly.
3. If the user wants to continue work, the Firefox tab-reuse bug (TO-DOS.md top item) is still the longest-standing open thread, now unresolved across two consecutive sessions — but per this session's own pattern, don't assume that's next; the user has been driving ad hoc requests against whatever page/file interests them each session, not necessarily working top-down through TO-DOS.md.

</current_state>
