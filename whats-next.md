<reading_instructions>
Whoever reads this document — a fresh Claude instance resuming this work, at the start of a new session — must lead their first response to the user with the contents of <current_todos> below, before summarizing <original_task>, <work_completed>, or anything else in this document.
</reading_instructions>

<current_todos>
# TO-DOS

## Footer nav links don't reuse an already-open tab in Firefox - 2026-08-20 14:11

- **Named-target footer links (`diagrams/FX_KW_spine.html`) aren't reusing an already-open destination tab in the user's actual Firefox browser, even though the tab was itself opened via the same link.** The three footer buttons — "Yijing Pathways", "FX circle / KW square", "Groups table" — each got a `target="..."` attribute this session (`target="yijing-pathways"`, `target="fx-circle-kw-square"`, `target="groups-table"`) specifically so that clicking one when its destination page is already open in another tab would return to/focus that tab instead of opening a new one, matching the pre-existing convention already used elsewhere in this project (`FX_circle_KW_square.html`'s own `target="fx-kw-spine"` and `target="groups-table"` links). **Problem:** verified working correctly in headless Chromium (`context.pages().length` stayed at 2 after clicking the same link twice — see the session's `test_targets.js` in a now-gone scratchpad, easy to recreate) — but the user, testing live in Firefox, reported the link still opens a brand-new tab on a second click, even after explicitly confirming (via the session's `AskUserQuestion`) that the already-open tab *was* itself opened by clicking that same link earlier — which was expected to be the one case where reuse should reliably work. The user had to leave mid-diagnosis, so this is unconfirmed/unresolved, not yet root-caused. **Files:** `diagrams/FX_KW_spine.html` (the three footer links, this session's new `target=` attributes); `diagrams/FX_circle_KW_square.html` (pre-existing `target="fx-kw-spine"`/`target="groups-table"` links on `spine-link-fx`/`spine-link-kw`/`unify-link` — worth checking whether *this* older pre-existing target-reuse behavior also fails for the user in real Firefox, or whether it's specific to the newly-added links, since that would narrow down whether this is a Firefox quirk with named targets in general vs. something specific to this session's change). **Solution:** not yet found — next session should first try to get a precise, minimal repro (e.g. a two-link toy HTML file) to isolate whether this is a Firefox-specific bug/setting around named-window-target matching (there's a real, documented Firefox preference `browser.link.open_newwindow` and related tab-vs-window handling that can affect this), whether it's specific to `file://` origins (already established this session that Firefox isolates each `file://` URL as its own origin, which broke other cross-tab approaches — worth checking if that isolation also affects named-target matching, not just storage/messaging APIs), or whether the *existing* `fx-kw-spine`/`groups-table` targets on `FX_circle_KW_square.html` have the exact same problem and it's simply never been noticed before. Ask the user to check Firefox's `about:preferences#general` tab-opening settings, and/or test target-reuse with a trivial two-page reproduction outside this project's actual files to isolate the variable.

## XianTian Circle Diagrams & Hexagram Group Table - 2026-08-12 13:01

- **Show the logical/systematic design of the XianTian trigram circle** - Make the construction logic of the trigram circle visible to a reader, not just its arrangement. **Problem:** The trigram circle (hero SVG in `index.html`, and the original `diagrams/xiantian-trigram-circle.svg`) currently shows the 8 trigrams correctly positioned and color-coded (self-reversing pair vs. mixed pair via two cross-axes), but a reader can't tell *why* they're arranged this way just by looking — the binary/yin-yang line logic and the self-reversing/mixed grouping aren't explained. **Files:** `index.html` (hero SVG, trigram glyphs now drawn as precise rects), `diagrams/xiantian-trigram-circle.svg`, `diagrams/FuXi21.html`. **Solution:** consider annotating the two cross-axes directly (label what "self-reversing" and "mixed" mean structurally), and/or surfacing the binary line values (111/110/101/100/011/010/001/000) that drive each trigram's position. **UPDATE (2026-08-21 session, see `<work_completed>` below):** this session did substantial work directly relevant to this TODO while brainstorming the group-table's numbering-system relationship — it exhaustively verified exactly which trigrams sit where and why (yang tetrad {Zhen,Li,Dui,Qian} = line-1-yang, occupies a clean contiguous 180° semicircle of the circle; yin tetrad {Xun,Kan,Gen,Kun} occupies the complementary semicircle) and connected this to the FX numbering scheme. None of this has been written into `xiantian-trigram-circle.svg` or `index.html`'s hero SVG yet (it lives only in this session's `Group-Table-properties.md`-track findings, not yet even written to a doc — see `<work_remaining>` below) — but it's now directly answerable and should make this TODO much faster to execute whenever it's picked up.

- **Show how the XianTian trigram circle maps concentrically outward to the XianTian hexagram circle** - Build a new diagram showing the traditional concentric-ring construction: inner ring = 8 trigrams, outer ring = 64 hexagrams. **Problem:** no existing diagram in this project shows this mapping — it's a structural relationship central to the FuXi/XianTian sequence work but currently undocumented visually. **Files:** new diagram, most likely alongside `diagrams/xiantian-trigram-circle.svg` / `diagrams/FuXi21.html`; may draw on `data/spreadsheets/FX-01.ods` for FX hexagram ordering data. **Solution:** reuse the rect-based trigram glyph technique from `index.html`'s hero (font-independent, pixel-precise) for the inner ring; verify hexagram line patterns the same way they were verified for the trigrams (render and read directly, don't recall from memory) before drawing the outer ring.

- **Link the trigram circle and hexagram circle diagrams together** - Once both diagrams above exist, connect them as one coherent piece rather than two independent artifacts. **Problem:** not yet decided whether this means a single combined SVG, or two separate pages/entries cross-linked. **Files:** wherever the two diagrams from the items above end up (likely `diagrams/`), plus the "Structure" strand entries in `index.html`. **Solution:** decide the linking approach once both diagrams are built.

- **Rebuild the hexagram Group Table starting from a spreadsheet** - Redo the Group Table work, this time using a spreadsheet as the canonical starting data source rather than the prior approach. **Problem:** the existing `notes/structure/Group-Table-properties.md` needs to be reworked from scratch with a spreadsheet-first workflow. **Files:** `notes/structure/Group-Table-properties.md`, `data/spreadsheets/FX-01.ods`, `data/spreadsheets/FX-01.xml`. **Solution:** use `data/spreadsheets/FX-01.ods` (or a fresh spreadsheet, if that one isn't the right starting point) as the source of truth for regenerating the group table data and derived properties. **Note:** this session added substantial new *analytical* content to `Group-Table-properties.md` (Observations 7–9, see below) on top of the existing spreadsheet-independent version — a future spreadsheet-first rebuild should make sure these observations (and the further ones from this session not yet written up) survive the rebuild or get re-verified against the new source.

## Trigram Circles, 3D Cubes & Central Taiji Page - 2026-08-13 22:08

- **Build a graphical representation of the FX and KW trigram circles together** - Create a new diagram showing the FuXi (XianTian) trigram circle and the King Wen (HouTian/latter-heaven) trigram circle side by side or otherwise paired, analogous to `diagrams/FX_circle_KW_square.html`'s FX-hexagram-circle/KW-hexagram-square pairing built this session. **Problem:** no diagram in this project currently shows the two trigram orderings (FuXi vs King Wen arrangement of the 8 trigrams) together or in comparison — only the single FuXi trigram circle exists (`diagrams/xiantian-trigram-circle.svg`, and the hero SVG in `index.html`). **Files:** new diagram (likely `diagrams/fx-kw-trigram-circles.html` following this session's naming convention), `diagrams/xiantian-trigram-circle.svg` (existing FX trigram circle to reuse/extend), `index.html` (hero SVG has the established rect-based trigram-glyph rendering technique — reuse it rather than reinventing). **Solution:** the King Wen trigram arrangement (post-heaven/HouTian bagua) is a different, well-known traditional ordering from the FuXi (pre-heaven/XianTian) one used in this project so far — will need its own verified trigram-position data, sourced and cross-checked the same rigorous way the FX↔KW hexagram bijection was (see `notes/structure/FX_to_KW.md`), not assumed from memory.

- **Show how the yin/yang groups between the FX and KW trigram circles relate** - Once both trigram circles exist, add the same kind of group-highlighting/equivalence feature built this session for the hexagram FX circle ↔ KW square (click-to-highlight, matching color, `UNIFY`-style cross-link) — but for the 8 trigrams' yin/yang groupings rather than the 64 hexagrams' quartets/pairs. **Problem:** not yet designed — unclear exactly what "yin/yang groups" means at the trigram level in this project's terms (e.g. pure-yang/pure-yin trigrams vs. mixed ones, or the FuXi self-reversing/mixed cross-axis grouping already noted as unexplained in the pre-existing "Show the logical/systematic design of the XianTian trigram circle" TO-DO above). **Files:** whatever new diagram is built for the item above; `diagrams/FX_circle_KW_square.html` as the interaction-pattern reference (its `showGroup`/`clearGroup`/`HEX_TO_GROUP`/display-box/`UNIFY`-link machinery). **Solution:** resolve the pre-existing open question about the trigram circle's self-reversing-vs-mixed cross-axis grouping first (see the first item in the "XianTian Circle Diagrams & Hexagram Group Table" TO-DO section above), since that's likely the same "yin/yang group" structure this item wants surfaced and compared against the KW trigram ordering. **UPDATE (2026-08-21 session):** this is now largely resolved in substance (not yet in any diagram) — see this session's pure/centered/mixed trigram categories (`Group-Table-properties.md` Observation 7) and the separate yang/yin-by-line-1 split (Zhen/Li/Dui/Qian vs Xun/Kan/Gen/Kun) explored later the same session. Both are directly applicable here.

- **Create 3D cube representations of the trigrams, "à la Z.D. Yung"** - Build a new visual/diagram representing each of the 8 trigrams as a 3D cube. **Problem:** the specific reference ("Z.D. Yung") and exact cube convention intended is not yet clear from this conversation alone — needs clarification from the user before design work starts (e.g. whether it's a known published diagram/book the user has in mind, what axes map to which of the 3 lines, whether yang/yin lines become filled/open cube faces or vertices, etc.). **Files:** new diagram, likely `diagrams/trigram-cubes-3d.html`; may want CSS 3D transforms (`rotate3d`/`perspective`) or an SVG-based pseudo-3D projection consistent with this project's existing SVG-rect line-glyph technique rather than pulling in a 3D library/dependency. **Solution:** ask the user for the source/reference for "Z.D. Yung" and the intended cube convention before implementing, since guessing wrong here would waste a full design-and-build cycle.

- **Build a central-Taiji page linking FX trigrams ↔ FX digrams ↔ Taiji ↔ KW digrams ↔ KW trigrams** - New page with the Taiji (yin-yang) symbol at its center, flanked outward on one side by FX digrams then FX trigrams, and on the other side by KW digrams then KW trigrams. **Problem:** "digrams" (2-line figures, the 4 possible combinations of two stacked yin/yang lines) are a new concept not yet represented anywhere in this project — only trigrams (3-line, 8 combinations) and hexagrams (6-line, 64 combinations) exist so far, so the digram data/ordering (both FX and KW variants) needs to be defined and verified from scratch, the same rigorous way trigram and hexagram data has been throughout this project (derive and cross-check programmatically, don't hand-type). **Files:** new page, likely `diagrams/taiji-trigrams-digrams.html`; `index.html` hero SVG and `diagrams/xiantian-trigram-circle.svg` for the existing rect-based line-glyph rendering technique to extend down to 2-line digrams and up to reused 3-line trigrams. **Solution:** clarify with the user what "FX digrams" vs "KW digrams" actually means (KW's traditional sequence is normally defined at the trigram/hexagram level, not digram level — the FX/KW digram distinction may need to be derived by the user's own logic, not an existing classical source) before building; likely depends on the "yin/yang groups" work above being resolved first, since the whole point of this page is showing the progressive binary construction (Taiji → digrams → trigrams) symmetrically for both orderings.

## KW Square Distance Markers - 2026-08-14 14:15

- **Add counting markers and distance brackets to the KW square** - Give `diagrams/kw-square.html` the same per-group distance annotation that `diagrams/FX_circle_KW_square.html` already has on the FX circle side. **Problem:** `FX_circle_KW_square.html` draws, per selected group, counting markers plus a bracket between paired members showing their distance apart (`buildDistanceLink()` around line 1752, drawing into the `#distance-overlay` `<g>`, populated on `showGroup()` and cleared via `overlay.innerHTML = ''` in `clearGroup()` — see the `.distance-link`/`.distance-tick`/`.distance-label-bg`/`.distance-label-text` CSS around line 126). `kw-square.html` has no equivalent yet. **Files:** `diagrams/kw-square.html` (to build); `diagrams/FX_circle_KW_square.html` (reference implementation, `buildDistanceLink()` and the `showGroup`/`clearGroup` pop-up wiring). **Solution:** port the same show-on-select/clear-on-deselect behavior, but note the KW square is a square grid, not a circle — `buildDistanceLink()`'s arcs (`arcPath()`, `.distance-link` paths) don't apply directly. The KW brackets need to be **straight lines with tick marks** (not arcs) — keep the tick/label-bubble parts of the pattern, replace the arc geometry with line geometry appropriate to the square layout.

**Note:** none of this session's work (see below) was itself a TO-DOS.md item being checked off — it was all ad hoc, user-directed extension of `diagrams/group-table.html` and `notes/structure/Group-Table-properties.md` beyond what's listed here. The file is otherwise unchanged this session except for the two "UPDATE" annotations added above, marking where this session's findings are now directly relevant to pre-existing items.
</current_todos>

<original_task>
This session opened with the user asking to read `whats-next.md`, a handoff from the prior session (2026-08-20), which had left `diagrams/FX_KW_spine.html` and `diagrams/group-table.html` with uncommitted changes (spine-bracket removal, font resizing, KW-distance badges) — that prior handoff's changes were found, at the start of *this* session, to have already been committed as `dfacacb` "Remove spine-side distance brackets, add KW-distance badges to group table" (evidently committed between sessions, outside this conversation).

From there, this session had two distinct phases:

**Phase 1 (concrete UI work on `diagrams/group-table.html`):** the user asked to (1) make all the "distance" badge values (both the circular FX badges and square KW badges in each group-table cell) selectable/clickable, with clicking a single distance value selecting its *entire* group including the paired axis's distance badge, and (2) fix a regression where this new behavior broke the pre-existing "Complementary lines 1 & 6" mode-box interaction (clicking a distance badge while that mode was active was cancelling the mode instead of respecting it).

**Phase 2 (open-ended structural brainstorming on `notes/structure/Group-Table-properties.md` and beyond):** the user then shifted into an extended, iterative brainstorming session — explicitly framed as "build, not prove" — exploring structural patterns in the FX Group Table: first the trigram-composition makeup of specific rows (leading to a new "pure/centered/mixed" trigram taxonomy), then how the table's four "center" rows (4–7) generate the six "peripheral" rows' categories and exact FX-sums, then (not yet written to any file) whether the project's FX hexagram-numbering *scheme itself* has a non-coincidental relationship to the group-table's structure — culminating in a King-Wen-numbering control test that empirically confirmed the FX/table relationship is not generic to "any numbering," and a terminology decision to describe the FX numbering as a "faithful" (structure-preserving) mapping of the Xiantian circle, rather than "efficient." The user had to break before deciding where (or whether) to write this final segment into the project's files, and asked explicitly to "keep this work" — this handoff is that preservation.
</original_task>

<work_completed>

## Phase 1 — `diagrams/group-table.html`: selectable distance badges

### 1. Made all FX and KW distance badges hover/click-active, selecting their whole group

- CSS: added `cursor: pointer; user-select: none;` to `.dist-badge` (the shared base class for both the circular FX badge and the square `.kw-dist-badge`).
- JS: added `cellFxList(cellEl)` (reads a cell's FX numbers straight from its `.set-label .num[data-fx]` spans) and `selectGroup(fxs, additive)` (mirrors the pre-existing single-hexagon `toggleSelect(fx, additive)` logic, but operates on a whole array: non-additive click replaces the selection with the group, or clears it on an exact-match second click; additive/Ctrl-click toggles the whole group in/out of the existing `selected` set without disturbing other selections).
- Wired every `.dist-badge` element (`document.querySelectorAll('.dist-badge')`) with `mouseenter`/`mouseleave` (preview the whole group's `.hl` highlight, un-highlighting on leave only for members not in `selected` — same convention as the existing single-hexagon hover) and `click`.
- Because both the FX and KW distance badges' highlight color was already driven by the pre-existing `.cell:has(.num.hl) .dist-badge` CSS rule (from the prior, already-committed session), no new CSS was needed for the badges to visually light up when their group is selected — only the JS selection logic was new.
- Updated the page's intro paragraph to mention the new interaction ("hover or click a distance badge to select its whole group, including the badge on the other axis").
- **Verified** via a from-scratch `jsdom` harness (see `<critical_context>` for why — no working browser was available): loaded the real `diagrams/group-table.html` file with `runScripts: 'dangerously'`, dispatched real `MouseEvent`s at specific `.dist-badge` elements, and asserted on the resulting `.hl` class states. Confirmed: clicking a badge highlights all of that group's FX numbers, KW numbers, and hex glyphs; clicking a different group's badge replaces the selection; clicking the same badge twice deselects (exact-match toggle-off); Ctrl-click adds a second group without clearing the first; clicking outside the table clears everything; hovering previews without persisting and un-highlights cleanly on mouseleave when nothing is selected.

### 2. Fixed: distance-badge click was cancelling the "Complementary lines 1 & 6" mode

- **Bug (user-reported):** the initial badge click-handler unconditionally cleared `activeMode` before selecting, so clicking a distance badge while the "Complementary lines 1 & 6" mode-box was active would silently deactivate that mode instead of respecting it.
- **Fix:** rewrote the click handler to mirror the pre-existing `wire()` function's own click logic exactly: `if (activeMode) { selectByMode(fxs[0], activeMode); } else { clearAxisHighlight(); selectGroup(fxs, e.ctrlKey); }` — i.e., when a mode is active, a badge click now calls the *existing* `selectByMode()` using a representative FX from the badge's own cell, which selects that group's own row *plus* its dual row under the mode's rule (e.g. the flip16 dual), exactly matching what clicking a hexagon/FX/KW number does under that mode.
- **Verified** via `jsdom`: activated `mode-flip16`, clicked a distance badge in row 1's left cell (FX{9,10,17,18}), confirmed the mode-box stayed `active` (not cancelled) and the highlighted FX set was exactly `[9,10,17,18,45,46,53,54]` — row 1's own group plus row 10's (its flip16 dual), matching row 10's actual FX{45,46,53,54} members read directly from the table.

## Phase 2 — Structural brainstorming, `notes/structure/Group-Table-properties.md`

### 3. Verified the user's original "pure/asymmetric" row-composition claims

User's claims: row 2 = "pure" + "asymmetric" trigrams; row 4 = "pure"; row 6 = "asymmetric"; rows 5, 7 = "asymmetric"; row 9 = "double asymmetric". Built `hex_data.json` by parsing every `<div class="hex" data-hex="N">` element's actual `<rect>` children in `diagrams/group-table.html` (not recalled from memory) to determine each of the 64 hexagrams' `line1`, `line6`, `lower_trigram`, and `upper_trigram` (trigram identity determined from the y-position/width pattern of the rects, per this project's existing rendering convention: `y="2.0"`=line6 (top) through `y="29.0"`=line1 (bottom); a single full-width rect = yang line, two half-width rects = yin line). Extracted the page's own `ROWS` JS variable (FX-number lists per row/axis) into `rows.json` by running the real page script inside `jsdom`. Under the interpretation "pure = Qian/Kun (uniform lines), asymmetric = the other six trigrams (uneven yin:yang split)," all six of the user's claims checked out exactly, on both axes, zero exceptions.

Flagged two issues back to the user: (1) "asymmetric" as defined (all 6 non-Qian/Kun trigrams) is a *broader* category than this doc's pre-existing "mixed" term (which only covers Zhen/Xun/Gen/Dui, excluding Li/Kan) — risk of term confusion; (2) row 9's "doubled" trigram property (both slots identical) isn't unique to row 9 — row 6 has it too, just on the *other* axis (axis A: FX37=Li/Li, FX38=Kan/Kan) where row 9 does *not* have it (row 9 is only doubled on axis B).

### 4. Terminology brainstorm (via `superpowers:brainstorming` skill, bounded path) → settled on pure/centered/mixed

Invoked the `superpowers:brainstorming` skill. User's first instinct was `pure` = Qian/Kun, `symmetric` = Kan/Li, `mixed` = Zhen/Dui/Xun/Gen, but flagged dissatisfaction with the names themselves. Asked one question at a time:
- Whether to anchor the {Kan, Li} pair's name in classical "middle son/middle daughter" family terminology (Kan/Li are the two "middle children" in the traditional Qian=Father/Kun=Mother/three-sons/three-daughters trigram-family assignment, which also explains structurally *why* they're palindromic — their one odd line sits in the *middle* position, line 2, rather than at an end) — user chose **geometric/invented instead**, not the classical anchor.
- Which specific geometric name for that pair — offered `centered`/`axial`/`nested`/`hinge` — user chose **`centered`**.

**Final settled terminology** (now written into `Group-Table-properties.md` as Observation 7):
- **pure** = {Qian, Kun} — all three lines identical (3:0 or 0:3 yin:yang split).
- **centered** = {Kan, Li} — two lines match, the odd line sits in the *middle* (line 2).
- **mixed** = {Zhen, Xun, Gen, Dui} — two lines match, the odd line sits at an *end* (line 1 or 3). Deliberately reuses the doc's pre-existing "mixed" term exactly (same 4 trigrams, same meaning) rather than redefining it.
- Noted explicitly: pure ∪ centered = the doc's pre-existing "self-reversing" set {Qian, Kun, Kan, Li} — this is a *refinement* of self-reversing, not a competing scheme.

### 5. Two of my own generalizations were wrong and had to be corrected by the user

While presenting the pure/centered/mixed design, I speculatively generalized beyond the six rows the user had actually asked about, and got it wrong: I claimed "rows 1 and 3 also turn out to be pure+centered mixes, just like row 2" (**wrong** — they're actually pure+**mixed**) and "rows 8, 10 are all-mixed too" (**wrong** — they're actually centered+**mixed**). The user caught both immediately: *"rows 1 & 3 = pure+mixed / rows 8&10 = centred+mixed."* Recomputed exhaustively (`full_scan2.py`) and confirmed the user's correction exactly. **Lesson (reinforcing this project's existing `feedback_verification-standard` memory):** an unverified extrapolation from one confirmed row's pattern to adjacent rows is exactly the kind of claim that needs the same exhaustive check as everything else — don't generalize from a spot-check.

### 6. Final, corrected, exhaustively-verified category-pair table (all 10 rows, both axes)

Every row has exactly one category-pair, identical on both axis tables:

| row | category-pair |
|---|---|
| 4 | pure + pure |
| 2 | pure + centered |
| 1, 3 | pure + mixed |
| 6 | centered + centered |
| 8, 10 | centered + mixed |
| 5, 7, 9 | mixed + mixed |

These are all six possible unordered pairs from {pure, centered, mixed} — confirmed exhaustively across all 64 hexagrams, zero exceptions. **This is now written into `Group-Table-properties.md` as Observation 7.**

### 7. Center-to-periphery generation (rows 4–7 as "center", 1–3 as "top", 8–10 as "bottom")

User's framing: the center rows (4–7) act as "essential/motivating pairs" that "radiate outward" to the top and bottom rows. Verified computationally (`center_radiate.py`): each of rows 4–7 is internally homogeneous (both trigram slots share one category on both axes) — row 4 = pure, row 5 = mixed, row 6 = centered, row 7 = mixed. Every pairing of two center rows, combining their essences, reproduces exactly one peripheral row's category-pair:

| center pair | combined essence | matches |
|---|---|---|
| {4,5} | pure + mixed | rows 1, 3 |
| {4,7} | pure + mixed | rows 1, 3 |
| {5,6} | mixed + centered | rows 8, 10 |
| {6,7} | centered + mixed | rows 8, 10 |
| {4,6} | pure + centered | **row 2 only** |
| {5,7} | mixed + mixed | **row 9 only** |

Cross-referenced against the doc's pre-existing "three-flip pattern" (Observation 2's "pair-block as index" — quartet duals 1↔10, 2↔9, 3↔8 already tied there to center-row splits {4,5}/{6,7}, {4,6}/{5,7}, {4,7}/{5,6} respectively). Found: the {4,6}/{5,7} split (2↔9's split) is the *only* one of the three whose two halves generate outputs that don't overlap with any other split's output — giving a structural explanation for the doc's pre-existing "Row 2 / row 9 asymmetry" (Observation 5). **This is now written into `Group-Table-properties.md` as Observation 8**, including a forward-reference to Observation 9 (below) noting that category alone can't distinguish row 1 from row 3, or row 8 from row 10 — only the exact sums (next finding) can.

### 8. FX-sum decomposition: exact arithmetic law, not just category matching

User's request: sum each group's own FX numbers, look for direct relationships, discriminating axis A (line1==line6) vs axis B (line1≠line6). Recomputed all 20 group sums directly from `rows.json` (not recalled) and found an *exact* law, not just a categorical one: each peripheral row's FX-sum equals precisely the sum of two specific center rows' FX-sums — the same generating pairs Observation 8 found categorically — on both axes, zero exceptions:

| peripheral row | = | center rows | axis A | axis B |
|---|---|---|---|---|
| row 1 | = | row 4 + row 5 | 54 = 3+51 | 78 = 31+47 |
| row 2 | = | row 4 + row 6 | 78 = 3+75 | 118 = 31+87 |
| row 3 | = | row 4 + row 7 | 126 = 3+123 | 134 = 31+103 |
| row 8 | = | row 5 + row 6 | 126 = 51+75 | 134 = 47+87 |
| row 9 | = | row 5 + row 7 | 174 = 51+123 | 150 = 47+103 |
| row 10 | = | row 6 + row 7 | 198 = 75+123 | 190 = 87+103 |

This is a complete bijection over all six unordered pairs of {4,5,6,7} — verified with a cross-check that the *alternate* possible generating pair for each ambiguous row (e.g. row 1 vs. the {4,7} pair that actually belongs to row 3) does *not* match, confirming specificity. This also **derives** (rather than just restates) the doc's pre-existing "shared constant across all duals" finding (row1+10 = row2+9 = row3+8 = rows4+5+6+7 = 252 on axis A / 268 on axis B, Observation 3): each quartet dual's two rows use complementary halves of {4,5,6,7} as generators (each center row used exactly once across the pair), so all three duals' sums are forced to equal the same total. **This is now written into `Group-Table-properties.md` as Observation 9.**

### 9. `Group-Table-properties.md` updated (committed to working tree, not yet git-committed)

Added Observations 7, 8, 9 (full text, tables, and cross-references as summarized above) and updated the "Overview" numbered list (now 1–9). Verified the file's heading structure parses cleanly after editing (`### 1` through `### 9`, `## Background`, `## Diagram` all present and correctly nested) via a small Python regex check.

### 10. Claim: FX odd/even numbering (yang=[1,3..63], yin=[2,4..64]) relates non-coincidentally to the group-table structure

User's claim 1: this relationship "is more than co-incidental." Verified via `parity_check.py` (reconstructing each hexagram's full 6-line pattern from its identified lower/upper trigram, using the standard trigram-to-3-bit table: Qian=111, Dui=110, Li=101, Zhen=100, Xun=011, Kan=010, Gen=001, Kun=000): **every one of the 32 consecutive FX(2k-1)/FX(2k) pairs is an exact full line-by-line inversion of each other** (the classical "opposite hexagram"/错卦 relationship), zero exceptions, for all k=1..32. Confirmed FX1/FX2 (Qian/Kun), FX9/FX10, FX63/FX64, etc.

Then checked whether "yang hexagram" could mean "majority of yang lines" — `yang_majority.py` found this does **not** hold universally: only 17/32 pairs have the odd member strictly yang-majority; 10 pairs are exact 3-yang/3-yin ties (FX15/16, 23/24, 27/28, 29/30, 39/40, 43/44, 45/46, 51/52, 53/54, 57/58); 5 pairs are outright reversed, i.e. the *odd*-numbered member is actually the yin-majority one (FX31/32, 47/48, 55/56, 59/60, 63/64). Flagged this to the user as the "majority" framing not surviving contact with the data, while the "exact opposite pair" framing does.

### 11. Claim: "yang hexagram" = hexagram whose line 1 (bottom line) is yang; grounded in the Xiantian circle's own yang/yin trigram split

User's claim 2, more precise: yang hexagram = line 1 is yang; XianTian yang trigrams = {Zhen, Li, Dui, Qian}; yin trigrams = {Xun, Kan, Gen, Kun}. Verified via `yang_line1.py`: confirmed all 8 trigrams' line-1 values match the stated yang/yin groupings exactly (checked against the bit table above, not assumed), **and** confirmed FX parity matches line-1's value for *all 64* hexagrams with **zero exceptions** — a clean, exceptionless criterion (unlike the "majority" framing above). This is the correct, precise version of claim 1.

### 12. Interaction between yang/yin-by-line-1, the axis A/B split, and the pure/centered/mixed rows

User asked to check how these interact. `interaction.py` found something stronger than expected: **every one of the 20 groups (10 rows × 2 axes) is composed *entirely* of whole consecutive opposite-pairs** (FX(2k-1)/FX(2k)), never a split pair — verified exhaustively (every member's opposite-partner is always present in the same group). Pair-rows (4,5,6,7) hold exactly 1 opposite-pair each; quartet-rows (1,2,3,8,9,10) hold exactly 2 each.

This single fact explains all three sub-questions at once:
1. **Why yang/yin is always exactly 50/50 in every group** — each opposite-pair contributes one yang + one yin member by definition.
2. **Why opposite-pairs never cross the axis A/B boundary** — flipping every line (including both line 1 and line 6 together) preserves whether line1==line6 or line1≠line6, since inverting both sides of an (in)equality preserves it.
3. **Why opposite-pairs never break a row's category-pair** — full line-inversion always maps each trigram to its own opposite *within the same category*: Qian↔Kun (pure↔pure), Li↔Kan (centered↔centered), Zhen↔Xun and Dui↔Gen (mixed↔mixed).

**None of findings 10–12 have been written into any project file yet** — see `<work_remaining>`.

### 13. Checked whether the numbering *choice* was historically motivated, or is more than a downstream correlation

User asked directly: is the FX/table relationship "more than a coincidence"? Read `notes/culture/Fuxi-sequence-origins.md` directly (not from memory) and found the load-bearing quote (original lines ~192–196): *"The odd/even (yang/yin) numbering convention this project adopted for the 64-hexagram circle... sits comfortably downstream of this — it's the project's own numbering choice layered onto the published diagram, not something independently attested in the historical record."*

Gave the calibrated answer: the relationship is "more than coincidental" because both FX-parity and the table's structure are *deterministic functions of the same underlying 6-line data* — not because of anything external. Any numbering built from line-1's value would automatically interlock with anything else in the table also built from line data.

User then pushed further: was the *choice* of line-1-based numbering itself motivated by something in the Xiantian tradition? Verified directly from this project's own already-recorded circle-position data (`Group-Table-properties.md`'s Background section: `[Qian, Xun, Kan, Gen, Kun, Zhen, Li, Dui]` at `[90, 45, 0, 315, 270, 225, 180, 135]` degrees): sorting by angle gives `Kan(0°,yin), Xun(45°,yin), Qian(90°,yang), Dui(135°,yang), Li(180°,yang), Zhen(225°,yang), Kun(270°,yin), Gen(315°,yin)` — **exactly two yin/yang transitions going around the circle**, i.e. the yang tetrad {Qian,Dui,Li,Zhen} and yin tetrad {Xun,Kan,Gen,Kun} each occupy one clean, unbroken 180° semicircle. Confirmed: this is a genuine, pre-existing, traditional geometric feature of the classical Xiantian circle — not something invented by the numbering scheme. Reconciliation offered: the specific integer *labels* (1, 3, 5...) are this project's own layer, but the structural feature those labels track (the circle's real hemisphere split) is inherited/traditional.

### 14. Tested whether "built, from the start, to encode" is a defensible historical claim — it is not

User asked me to check this specific wording for consistency. I flagged the gap between *consistency* (verified) and *intent* (unverified) — a binary encoding with line 1 as the least-significant bit would produce the same parity-match as an almost-automatic arithmetic consequence, regardless of whether "encoding the circle" was ever a deliberate goal. Dispatched an async Explore-agent search of the whole project for any documented rationale behind the FX-numbering rule.

**Agent's findings (now folded in here):**
- No file anywhere in the project documents *why* odd=line1-yang was chosen, or the binary-encoding rule's construction logic in prose at all.
- `notes/culture/Fuxi-sequence-origins.md:192-196` explicitly frames the numbering as **"the project's own numbering choice"** — deliberate, but with no stated rationale.
- `TO-DOS.md` (the "Show the logical/systematic design of the XianTian trigram circle" item, see `<current_todos>` above) and the prior `whats-next.md` both already flagged the trigram circle's own construction logic as an open, never-written-up gap.
- `notes/structure/FX_to_KW.md:114-118` states the FX ground truth was parsed empirically from rendered SVG glyphs, not derived from a stated generative rule.
- Reverse-engineering the raw `HEXLINES` table in `diagrams/FX_circle_KW_square.html:1739` (the agent's own observation, not project-documented) suggests FX1–16 has the lower trigram alternating fixed Qian/Kun while the upper trigram counts in binary — but this is inference from data, not documented reasoning.

**Conclusion:** "built, from the start, to encode a genuine pre-existing feature" is **not verifiable as historical fact** and should not be recorded as one. Offered two paths: leave it an open question, or explicitly adopt it as **the project's own stated design rationale going forward** (not recovered history). **User chose the second, explicitly: "point 2 is the easy and desirable choice... proceed with that as basis."**

### 15. King Wen control test — the decisive empirical finding

User pushed back further: the table's *grouping structure* is numbering-independent (correct — it would look identical under any relabeling), so is the FX/table relationship really non-generic, or would *any* numbering show it? Proposed and ran a control test using King Wen numbering (already present in the project via the `FX_TO_KW` mapping embedded in `diagrams/group-table.html`), re-running the exact same three tests from findings 10–12 but with KW numbers substituted for FX numbers:

| test | FX | KW |
|---|---|---|
| parity matches line 1 | 64/64 | 38/64 (≈chance) |
| adjacent pairs (2k-1,2k) are opposite-hexagrams | 32/32 | 8/32 (≈chance) |
| peripheral row = sum of 2 center rows | 12/12 | **0/12** |

**This is decisive.** King Wen numbering — which this project's own prior research (`Fuxi-sequence-origins.md`) already established has no known derivation ("the reasoning, if any, that informs [the King Wen] sequence is unknown") — fails all three tests at or near chance level, while FX passes all three exactly. This proves the FX/group-table relationship is *not* a generic property any numbering would exhibit relative to this table's structure; it is a specific, verified consequence of FX's own line-data-based construction. The user called this "exactly the sort of claim which will motivate a reader to continue on into this project" and asked that it be preserved for future write-up.

### 16. Terminology settled: "faithful" (or technically, "structure-preserving"), not "efficient"

User asked whether "the numbering system maps onto the FX hexagram circle efficiently" is defensible phrasing. Reaction: "mapping" is fine (a numbering *is* technically a bijection/mapping — true of KW too, trivially), but "efficiently" doesn't capture what was actually verified and invites the wrong kind of scrutiny ("efficient by what measure, compared to what?"). The precise, falsifiable claim is about **structure preservation**: FX's mapping carries the circle's real relationships (hemisphere membership → parity; opposite-hexagram pairs → adjacent integers; additive group structure → exact sums) intact into arithmetic, and the King Wen control test (finding 15) just proved this isn't automatic for any mapping. Suggested "structure-preserving" (technical) or **"faithful"** (plain-English) as the correct adjective, with a candidate sentence: *"The numbering system is not an arbitrary label — it's a structure-preserving mapping of the Xiantian circle: the circle's real geometric and combinatorial relationships survive intact in the arithmetic of the numbers themselves."* **User agreed explicitly: "I agree to 'faithful', good suggestion."**

</work_completed>

<work_remaining>

## Highest priority: write up findings 10–16 (Phase 2's second half) into the project — location not yet decided

**Nothing from findings 10 through 16 above (everything from "is the FX/table relationship more than coincidental" onward) has been written into any project file yet.** It exists only in this conversation and in this handoff document. The user had to break immediately after agreeing to "faithful" as the settled terminology, without deciding *where* this should be written up. Next session should ask the user (or use judgement if they don't have a strong preference) among:

1. **A new Observation (10, 11, ...) in `notes/structure/Group-Table-properties.md`**, continuing the existing numbered-observation pattern, covering: the exact-opposite-pair law for all 32 FX pairs (finding 10, with the "majority yang lines doesn't hold" caveat noted as a *rejected* framing, not a live claim); the line-1-exact-criterion (finding 11); the "opposite-pair is the table's atomic unit" finding and its three explanatory consequences (finding 12); the King Wen control test (finding 15, arguably the single most valuable result to preserve verbatim, per the user's own comment about it being "the sort of claim which will motivate a reader to continue").
2. **An addition/refinement to `notes/culture/Fuxi-sequence-origins.md`'s "Implications for this project" section** (around its existing line ~192-196 bullet about the numbering convention), since findings 13–16 directly extend and sharpen that section's existing claim, and that file is specifically the project's home for numbering-scheme provenance/rationale discussion.
3. **Both, cross-linked** — structural/mathematical findings (10, 11, 12, 15) in `Group-Table-properties.md`; the historical/rationale framing (13, 14, 16, including the explicit "faithful mapping, adopted as this project's own stated design choice" framing) in `Fuxi-sequence-origins.md`, with each pointing to the other.

Whichever location(s), the write-up should explicitly capture:
- The exact tables/numbers reproduced in `<work_completed>` findings 10, 12, 15 above (all independently re-derivable from `diagrams/group-table.html`'s own rendered data, per this project's verification standard — see `<critical_context>`).
- The corrected framing history: "majority yang lines" was tried and explicitly rejected (10 ties + 5 reversals) in favor of the exact "line 1 = yang/yin" criterion (zero exceptions) — worth keeping both in the writeup, since the rejected framing is itself informative about why the final one is the right one.
- The King Wen control test as the load-bearing piece of evidence, not just an aside.
- The explicit, quoted user decision to adopt "the numbering was built to encode the circle's real structure" as this project's own *stated design rationale going forward*, not as a claim about recovered 11th-century (or earlier) historical intent — distinct from, and should not be conflated with, the file's separate, more skeptical historical-provenance research already in `Fuxi-sequence-origins.md`.
- The settled terminology: **"faithful"** (or "structure-preserving" if a more technical register is wanted) — not "efficient", which was explicitly considered and rejected.

## Also still open

- **Commit the two currently-uncommitted files** (`diagrams/group-table.html`, `notes/structure/Group-Table-properties.md`) — no commit was made or requested this session; per this project's established `feedback_push-reminder` pattern, remind the user before ending a session, but let them drive the actual commit.
- **Visually verify `diagrams/group-table.html`'s new distance-badge selectability in the user's real Firefox** — this session's verification was entirely via `jsdom` simulation (see `<critical_context>` for why), never a real browser. Given this project's well-established history of Chromium-vs-Firefox rendering/behavior discrepancies, this is worth a live check, especially the `:has()`-based highlight-coloring CSS (already flagged as Firefox-compatible from a prior session, but worth reconfirming with this session's new interaction paths).
- All of `<current_todos>` above remains open except for the two "UPDATE" annotations added this session (marking where new findings are now directly relevant) — the Firefox tab-reuse bug is still the longest-standing, oldest unresolved item.
- Consider whether findings 10–12 (the yang/yin-by-line-1, opposite-pair, and circle-semicircle work) should also feed directly into the **first** `TO-DOS.md` item under "XianTian Circle Diagrams & Hexagram Group Table" ("Show the logical/systematic design of the XianTian trigram circle") — this session's work answers exactly the question that TODO poses (why the trigrams are arranged as they are), just not yet drawn into the diagram itself. See the "UPDATE" annotation already added to that TODO item above.

</work_remaining>

<attempted_approaches>

- **MCP Playwright browser tool was unusable all session** — `mcp__plugin_playwright_playwright__browser_navigate` requires the `"chrome"` channel specifically; `npx playwright install chrome` fails needing root/sudo with no interactive terminal available in this sandboxed environment ("Switching to root user to install dependencies... sudo: A terminal is required to authenticate"). Worked around by running `npx playwright install chromium` instead (succeeded, downloaded a headless-shell Chromium build to `~/.cache/ms-playwright/`), but this does **not** satisfy the MCP tool's specific chrome-channel requirement, so the MCP browser tools remained unusable regardless of this workaround. **Actual solution used instead:** installed `jsdom` locally via `npm install jsdom --no-save` inside the scratchpad directory, then loaded and ran the real `diagrams/group-table.html` file (including its actual embedded `<script>`) with `runScripts: 'dangerously'`, dispatching real `MouseEvent`s and reading back DOM state — this became the primary/only verification method for all JS-behavior checks this session, in place of a real browser.
- **My own two incorrect generalizations** (see `<work_completed>` finding 5) — claimed rows 1, 3 were "pure+centered" and rows 8, 10 were "all-mixed" by pattern-matching from row 2's and rows 5/7/9's confirmed patterns respectively, without actually checking rows 1, 3, 8, 10 directly first. Both wrong; user caught both immediately. Corrected via an exhaustive per-row-per-axis recomputation (`full_scan2.py`) rather than patching the specific wrong claims in place — re-verify-from-scratch was faster and safer than trying to figure out exactly which parts of the wrong generalization were salvageable.
- **Considered "asymmetric" as a single broad category name** (= all 6 non-Qian/Kun trigrams) during the early part of the terminology brainstorm — internally consistent for the user's original 6 claims, but abandoned once the user wanted the {Kan,Li} pair distinguished from {Zhen,Xun,Gen,Dui} explicitly (leading to the 3-way pure/centered/mixed split instead). "Asymmetric" does not appear anywhere in the final, written Observations 7–9.
- **Considered anchoring the {Kan,Li} category name in classical "middle son/middle daughter" family terminology** (Qian=Father/Kun=Mother/three-sons/three-daughters trigram-family assignment) — genuinely applicable and would have explained the palindrome property structurally, but the user explicitly preferred a geometric/invented term instead (leading to "centered"). Not used, but worth remembering as a real, available alternative if "centered" ever needs revisiting.
- **Considered whether "majority of yang lines" defines a yang/yin hexagram** — tested exhaustively and explicitly rejected (10 ties, 5 reversals out of 32 pairs) in favor of the exact "line 1 = yang/yin" criterion. This rejected framing is itself worth keeping in any write-up (see `<work_remaining>`), since it's informative about why the final framing is the right one, not just a discarded false start.
- **Considered claiming the numbering was "built, from the start, to encode" the circle's structure as literal historical fact** — tested via an Explore-agent search of the entire project for supporting documentation, found none exists, and the claim was explicitly downgraded from "historical fact" to "adopted, going forward, as this project's own stated design rationale" at the user's own direction (see `<work_completed>` finding 14).

</attempted_approaches>

<critical_context>

## Data/verification infrastructure built this session (scratchpad-local, not permanent)

All computation this session happened in `/tmp/claude-1000/-home-greg-pCloudDrive-YIJING-Yijing-Pathways/58f4c86d-dfee-4e87-ae6b-5362c72b21e7/scratchpad/` — a session-specific directory that may not persist. Key artifacts, easily regenerable if lost:
- **`hex_data.json`** — per-FX-number (1–64) `line1`, `line6`, `lower_trigram`, `upper_trigram`, derived by parsing the actual `<rect>` elements inside each `.hex[data-hex="N"]` in `diagrams/group-table.html` (y-position/width pattern → yin/yang per line; the six line-rows sit at `y="2.0"` (line 6, top) through `y="29.0"` (line 1, bottom), drawn top-to-bottom as line6→line1 — an already-established convention from a prior session, re-verified this session). **Regeneration method, if needed again:** regex over the HTML for `<div class="hex" data-hex="(\d+)">...</div>`, then per-hexagram regex over its `<rect>` children grouped by `y` attribute, single-rect-width-18 = yang / two-rects-width-7 = yin.
- **`rows.json`** — the 10-row × {A,B}-axis FX-number lists, extracted by loading the real `diagrams/group-table.html` in `jsdom` with `runScripts: 'dangerously'` and reading out its own `ROWS` JavaScript variable directly (rather than re-parsing the HTML a second, independently-fallible way) — this is the *exact* same `ROWS` structure the live page's own JS uses for `groupsForMode()`/`selectByMode()`, so it's guaranteed consistent with the page's actual behavior, not a separate reconstruction.
- The standard trigram-to-3-bit table used throughout (bottom-to-top, yang=1/yin=0): `Qian=(1,1,1), Dui=(1,1,0), Li=(1,0,1), Zhen=(1,0,0), Xun=(0,1,1), Kan=(0,1,0), Gen=(0,0,1), Kun=(0,0,0)`.
- The `FX_TO_KW` mapping used for the King Wen control test (finding 15) was extracted directly from `diagrams/group-table.html`'s own embedded `var FX_TO_KW = {...}` JS object via regex — not retyped, guaranteed consistent with the live page.

## Process notes

- The `superpowers:brainstorming` skill was invoked once (for the pure/centered/mixed terminology decision, finding 4) and completed its **bounded** path in full: context exploration, two one-at-a-time clarifying questions via `AskUserQuestion`, a short in-chat design presentation (which included the two wrong generalizations later corrected), and consolidation on explicit user request ("let's consolidate this") — no separate spec file was written, consistent with the skill's bounded-task process.
- The rest of Phase 2 (findings 10–16) proceeded as free-form, non-skill-invoked "claim → verify → react" brainstorming per the user's own explicit framing ("my motivation is not to 'prove' but to 'build'... if my claims are consistent that's a plus") — each user claim was tested computationally against the actual project data before reacting, consistent with this project's `feedback_verification-standard` memory, but the *tone* throughout was collaborative reaction/refinement rather than adversarial fact-checking.
- One async `Explore` agent was dispatched (finding 14) to search the whole project for FX-numbering-rule documentation; it returned precise file/line citations (folded into finding 14 above) and, notably, *confirmed an absence* (no such documentation exists) rather than finding a positive answer — that negative result was itself the useful and actionable one.

## Key reconciliation to preserve precisely (finding 14/16, easy to conflate if reconstructed from memory)

There are **two different, non-conflicting claims in play**, and any future write-up must keep them separate:
1. **A historical/provenance claim** (skeptical, evidence-based, matches `Fuxi-sequence-origins.md`'s existing tone): no documentation exists anywhere establishing *why* this project's FX-numbering rule was originally defined the way it was, or that it was deliberately designed "from the start" to track the Xiantian circle's hemisphere structure. This remains true and should not be overwritten by an enthusiastic-sounding rewrite.
2. **A going-forward design-rationale claim** (the user's explicit, adopted choice this session): *regardless* of what the original, undocumented historical motivation was, this project now explicitly adopts "the numbering is a faithful/structure-preserving encoding of the Xiantian circle's real structure" as its own stated rationale for the numbering scheme, backed by the King Wen control test as empirical support that this property is real and non-generic (finding 15). This is a decision made *in this session*, not a discovery about the past.

Any write-up should make claim 2 clearly a project-level design statement, explicitly distinguished from claim 1's historical skepticism — conflating them would misrepresent both the existing `Fuxi-sequence-origins.md` research and this session's own findings.

## Relevant persistent memory (see `/home/greg/.claude/projects/-home-greg-pCloudDrive-YIJING-Yijing-Pathways/memory/`)

`feedback_verification-standard` (applied rigorously and repeatedly this session — every trigram/line/sum claim checked exhaustively against the page's own rendered data, not recalled), `feedback_handoff-staleness-check` (this handoff's own `<work_completed>` §Phase 1 opening notes that the *prior* handoff's described uncommitted work had already been silently committed as `dfacacb` before this session began — re-confirms the pattern that memory flags), `feedback_whats-next-leads-with-todos` (followed — see `<reading_instructions>`), `feedback_push-reminder` (applies — two files uncommitted, flagged above, no commit made or requested), `project_github-setup`, `project_spine-page-css-gotcha` (not directly relevant this session, no spine-page work), `project_asana-removed`, `reference_pcloud-backups`, `reference_obsidian-vault`, `user_extreme-zoom-out-viewing` (not directly invoked this session, no new font/legibility work).

</critical_context>

<current_state>

## Git status

```
$ git status --short
 M diagrams/group-table.html
 M notes/structure/Group-Table-properties.md
```

```
$ git diff --stat
 diagrams/group-table.html                 |  63 ++++++++++++++-
 notes/structure/Group-Table-properties.md | 125 ++++++++++++++++++++++++++++++
 2 files changed, 187 insertions(+), 1 deletion(-)
```

`diagrams/FX_KW_spine.html` — no longer modified; the prior session's changes to this file (described as pending in the previous `whats-next.md`) were already committed as `dfacacb` before this session began. **No commit or push has been made or requested during this session.**

## Deliverable status

- **`diagrams/group-table.html`**: distance badges (both FX circle and KW square) are now fully selectable, individually and as whole-group selections, with correct interaction under the "Complementary lines 1 & 6" mode. Verified via `jsdom` simulation only — not yet confirmed in a real browser.
- **`notes/structure/Group-Table-properties.md`**: Observations 1–6 unchanged (pre-existing); Observations 7 ("Pure / centered / mixed trigram categories"), 8 ("Center-to-periphery generation"), and 9 ("FX-sum decomposition: peripheral rows = center-row pairs") newly written this session, with the Overview list updated to list all 9. Heading structure verified to parse cleanly.
- **Findings 10–16** (yang/yin-by-line-1 exact criterion, opposite-pair-as-atomic-unit, the historical numbering-rationale research, the King Wen control test, and the "faithful" terminology decision): **fully documented in `<work_completed>` of this handoff, but not yet written into any actual project file.** This is the top priority for the next session — see `<work_remaining>`.
- **`TO-DOS.md`**: unchanged in substance; two "UPDATE" annotations added within `<current_todos>` above (not yet propagated to the actual `TO-DOS.md` file on disk — that file itself was **not edited** this session, only referenced/reproduced here; if the user wants those UPDATE annotations to persist in the real `TO-DOS.md`, that edit still needs to be made).
- **`whats-next.md`** (this file): this refresh, written at explicit user request ("I have to break now. Please keep this work...") to preserve everything before context is lost, per the `whats-next` skill's comprehensive-detail mandate.

## Immediate next step for whoever resumes

1. Greet/resume with the user, lead with `<current_todos>` as instructed.
2. Ask the user where findings 10–16 should be written up (the three options in `<work_remaining>`'s first section), or use judgement if they'd rather you just proceed — they were mid-decision on this when they had to break, not blocked on it for lack of information.
3. Note: the "UPDATE" annotations added to `<current_todos>` above exist only in this handoff document, not in the real `TO-DOS.md` on disk yet — decide with the user whether those should be written back to `TO-DOS.md` itself.
4. Per `feedback_push-reminder`, remind the user that `diagrams/group-table.html` and `notes/structure/Group-Table-properties.md` are still uncommitted — but only *remind*, don't commit unprompted.

</current_state>
