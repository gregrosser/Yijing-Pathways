<reading_instructions>
Whoever reads this document — a fresh Claude instance resuming this work, at the start of a new session — must lead their first response to the user with the contents of <current_todos> below, before summarizing <original_task>, <work_completed>, or anything else in this document.
</reading_instructions>

<current_todos>
# TO-DOS

## Continue Editing the New FX_KW_spine Page - 2026-08-19 13:49

- **Continue building out `diagrams/FX_KW_spine.html`** - This is a brand-new page (built this session) reached via the "FX SPINE"/"KW SPINE" links added to `diagrams/FX_circle_KW_square.html`'s spine-link-group box. It embeds the full FX and KW body-schema spine SVGs (copied from `diagrams/spine03/Spine_Page5_Both.html`) and, driven by a `?fx=1,2,63,64`-style query string set by `FX_circle_KW_square.html` when a group is selected, highlights (fills) just that group's curve in each panel while leaving every other curve unfilled for context, and draws a vertical "distance" bracket beside each panel (circle label left of the FX spine, square label right of the KW spine) showing the group's canonical FX/KW distance (reusing the exact `GROUPS`/`kwGroupDistance` logic from `FX_circle_KW_square.html`, not a re-derived value). **Problem:** this session ended mid-build. The explicitly-planned next step is: insert hexagram display boxes at "bottom-centre" of the page — the panel gap was already widened by 60% (200px→320px `--page-gap`) specifically to make room for these, but the display boxes themselves were never added. Nothing in this session's `FX_KW_spine.html` work has been committed or pushed yet either. **Files:** `diagrams/FX_KW_spine.html` (the page itself, ~213KB, generated — do not hand-edit the huge embedded SVG blocks directly); `diagrams/FX_circle_KW_square.html` (source of the `?fx=...` query param via `spine-link-fx`/`spine-link-kw` hrefs, and of the canonical `GROUPS`/`FX_TO_KW` data reused on the new page); `diagrams/spine03/Spine_Page5_Both.html` (source of the two embedded spine SVGs). **Solution:** the page was built via a Python generator script at a session-scoped scratchpad path (`/tmp/claude-.../scratchpad/build_fx_kw_spine.py`) that spliced the two spine SVGs from `Spine_Page5_Both.html` and wrapped them with new CSS/HTML/JS — that script no longer exists in a fresh session, so further edits should either hand-edit `diagrams/FX_KW_spine.html` directly (it's plain HTML/CSS/JS, just large) or reconstruct an equivalent generator; either way, verify changes computationally (headless-browser measurement, per this project's standing verification standard) rather than eyeballing, the same way every prior round of edits to this page was checked this session. Also note a bfcache-safety pattern already established on this page (`window.addEventListener('pageshow', update)`) — preserve it if refactoring the page's script.

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
This session opened with the user asking to read `whats-next.md` (the handoff from the prior session, which was itself found to be 5 commits stale — the prior session's own work had already been committed and pushed, and `TO-DOS.md` had moved on since that document was written). After reporting the corrected current TO-DOS list, all further work this session fell into two phases:

**Phase 1** — a long, iterative sequence of small, precise UI-refinement requests against `diagrams/FX_circle_KW_square.html` (title sizing/gap/centering, FX-circle/KW-square vertical alignment, a new two-link "spines box" navigation feature, arrow-icon add-then-remove, border-width tweaks, panel-title renames, hexagram hover-highlight). This phase was committed and pushed mid-session (commit `222af4a`).

**Phase 2** — building a brand-new page, `diagrams/FX_KW_spine.html`, reached via the "FX SPINE"/"KW SPINE" links added in Phase 1. This page shows the full FX-inversion-spine and KW-complement-spine body-schema diagrams (reusing verified SVG content from `diagrams/spine03/Spine_Page5_Both.html`), with the single hexagram group most recently selected on `FX_circle_KW_square.html` highlighted and a "distance" bracket drawn beside each panel. This phase went through several rounds of user-driven refinement (see `<work_completed>`) and is **not yet committed**.

The session ended with two explicit user requests: (1) add a top-priority `TO-DOS.md` entry to continue the `FX_KW_spine.html` work, and (2) refresh this handoff document.
</original_task>

<work_completed>

## Phase 1 — `diagrams/FX_circle_KW_square.html` polish (committed as `222af4a`, pushed to `origin/master`)

Covered extensively in the *previous* version of this handoff (now superseded/overwritten — see `<critical_context>` below for where to find it if needed). Summary: panel-title sizing/centering fixes, FX-circle/KW-square vertical-center alignment, a new "spines box" (originally "TO FX SPINE"/"TO KW SPINE", ending as plain "FX SPINE"/"KW SPINE") stacked above a renamed "TABLE" link (was "UNIFY"), FX-hexagram hover-highlight (`.hex-hover` class, both trigram halves highlight together), and various border/arrow/spacing iterations. All verified via a headless-Chromium/Playwright measurement harness in the scratchpad directory. This work is safely on `master` already; no further action needed on it.

**One small Phase-1 follow-up change happened in Phase 2** (not yet committed): `showGroup()` in `FX_circle_KW_square.html` (~line 2087-2090) was extended to also set `spine-link-fx`/`spine-link-kw`'s `href` dynamically, e.g. `'FX_KW_spine.html?fx=' + sortedFx.join(',') + '#fx'`, mirroring the pre-existing `unifyLink.href = 'group-table.html?fx=' + sortedFx.join(',')` pattern. This is the *only* uncommitted change in this file — a 2-line diff, `git diff diagrams/FX_circle_KW_square.html` confirms it's just these two new lines.

## Phase 2 — `diagrams/FX_KW_spine.html` (new file, entirely uncommitted)

Built and iteratively refined via a Python generator script at `/tmp/claude-1000/-home-greg-pCloudDrive-YIJING-Yijing-Pathways/30dab904-284f-44ea-bb39-9bdfac044e68/scratchpad/build_fx_kw_spine.py` — **this path is session-scoped and will not exist in a fresh session.** The script spliced the two full spine `<svg>` blocks out of `diagrams/spine03/Spine_Page5_Both.html` (byte-identical to the source, just with `id="fx-spine-svg"`/`id="kw-spine-svg"` injected on the root `<svg>` tags) and wrapped them in new page chrome. Every round below was re-run through this script then re-verified in a headless browser before moving to the next request; nothing was eyeballed.

### 2.1 — Initial page (request: "make a start... only the selected group is shown")
- First attempt hid every group/hexagram marker except the selected group's (via `display:none`), auto-cropping each panel's `viewBox` to the visible content's bounding box.
- **Verified structural discovery, load-bearing for everything after:** every one of the 148 top-level children of each spine `<svg>` carries an `inkscape:label` attribute. 20 of them per panel match `/^FX\{[\d,]+\}$/` (or `KW{...}`) and are the group-connector "curve" shapes — together their member-lists exactly partition all 64 hexagram numbers with no overlaps or gaps. The other 128 match `/^FX_(left|right)NumCirc_\d+$/` (or `KW_...`) and are the individual hexagram-number badges (a small circle + `<text>` showing the hexagram's own number), each containing a `<text>` element that must be read to know which hexagram it actually displays — the numeric suffix on the id is a **row/position index**, not necessarily the hexagram value, though in the specific quartet tested (`FX{3,4,63,64}`) they happened to coincide. **This was cross-checked programmatically against `FX_circle_KW_square.html`'s live `GROUPS`/`FX_TO_KW` data** (dumped via a headless-browser `window.GROUPS`/`window.FX_TO_KW` evaluation to `/tmp/fxkw_dump.json` — also session-scoped/gone) and found to match exactly, both directly (FX side) and after mapping through `FX_TO_KW` (KW side).

### 2.2 — Correction (request: "much too empty... include all the symmetric curves... only the selected group's curves are filled")
- Reworked to **never hide anything** — all 20 group-curves and all 128 numCirc badges in both panels are always rendered. Instead, JS restyles: every group-curve's descendant elements get `fill:none; stroke:var(--ink-faint)` (dim/unfilled) except the one matching the selected group, which gets `fill:var(--seal); stroke:var(--seal)` (filled/highlighted). Critical implementation detail: each curve's fill/stroke must be set on **every descendant element**, not just the top-level `<g>`, because Inkscape's SVG export gives each child `<path>` its own explicit `fill`/`stroke` inline style that does not inherit from an ancestor's style — `styleCurve()` does `[el].concat(el.querySelectorAll('*'))` and sets style on all of them.
- Removed the earlier `viewBox` auto-cropping entirely (no longer relevant once nothing is hidden) — both panels always show their original, full, unmodified `viewBox`.
- No-selection state (`FX_KW_spine.html` with no `?fx=` param) shows the full spine with every curve dimmed/unfilled plus a visible `#empty-note` message; does **not** hide the diagrams.

### 2.3 — Panel gap increase (request: "increase the gap between FX-spine and KW-spine by 60%... but first only increase the gap")
- `--page-gap` (a `:root` custom property controlling `.page-columns`'s grid `column-gap`) changed from `200px` to `320px` (exactly 1.6×, verified via `getComputedStyle(...).columnGap`).
- Explicitly **not yet acted on**: the stated purpose of this gap increase — making room for hexagram display boxes at "bottom-centre" — was flagged by the user as a *future* step, not this round's task. Noted as a side effect: the wider gap narrowed the KW panel's grid column enough that "King Wen" now wraps to two lines in its name-tag box; left as-is since not asked about.

### 2.4 — Distance brackets (request: vertical bracket + ticks + circle-labeled distance left of FX-spine; same but square-labeled, right of KW-spine, "similar to the KW-square bracket")
- Added `.spine-frame` wrapper divs around each spine `<svg>` (`fx-spine-frame`/`kw-spine-frame`), each with a reserved gutter (`padding-left`/`padding-right`) and an absolutely-positioned overlay `<svg id="fx-distance-overlay">`/`#kw-distance-overlay` for drawing into, directly analogous to `FX_circle_KW_square.html`'s `.kw-square-frame`/`#kw-distance-overlay` pattern (which was consulted as the explicit reference implementation).
- `drawDistanceBracket()` draws: a vertical line + top/bottom ticks spanning the topmost-to-bottommost Y position of the selected group's *visible* numCirc badges in that panel, plus a centered label (circle for FX, square for KW, matching this project's established FX=circle/KW=square convention) showing a "distance" number.
- **This round's distance number was wrong** (see 2.5) — computed as `(maxRowIndex − minRowIndex + 1)` from the numCirc id suffixes, which the user caught was exactly double the correct value in both directions.

### 2.5 — Distance-number fix + stroke-width + font-size (request: "distance numbers are 2×... make bracket line-width 2.5px... font-size 300% larger")
- **Root-caused and fixed properly, not just patched by dividing by 2.** The correct distance values are the *pre-existing, already-verified* `GROUPS[].distance` field (FX side, quartets only; pairs are always distance 1 by established convention) and a `kwGroupDistance()`/`kwPairIndexRange()` computation (KW side) — both copied verbatim from `FX_circle_KW_square.html`'s own logic, not re-derived. The full `GROUPS` array (20 entries, with `members`/`type`/`distance`/`pairs`/etc., dumped from the live page via the same `/tmp/fxkw_dump.json` snapshot used in 2.1) is now embedded directly in `FX_KW_spine.html`'s `<script>`. A `findGroup(fxSet)` helper matches the URL's `?fx=` set against `GROUPS[].members` to find the exact group object, then `fxGroupDistance(g)`/`kwGroupDistance(g)` compute the correct numbers. Verified against both a quartet (`{3,4,63,64}` → FX 31, KW 11 — previously wrongly showed 62/22) and a pair (`{1,2}` → 1/1 both sides — previously wrongly showed 2/2).
- Bracket stroke-width: `1.5px` → `2.5px` on `.distance-bracket-line`, `.distance-tick`, `.distance-label-bg`.
- Label font-size: `16px` → `64px` (exactly 4×, i.e. "300% larger"). **Incidental fix required and applied without being asked:** the enlarged label no longer fit in the original 40px gutter and was being clipped at the page/viewport edge (confirmed via `getBoundingClientRect()` showing the label's right edge past `window.innerWidth`). Fixed by widening `.fx-spine-frame`'s `padding-left` and `.kw-spine-frame`'s `padding-right` from `40px` to `140px`, and moving the bracket's `lineX`/`tickX` positions outward to `70`/`100` (from `18`/`30`) to center the now-larger label within the wider gutter. Label radius is computed proportionally to font-size using the same ratio (`15/16`) `FX_circle_KW_square.html` itself uses, so it will continue to stay proportional if font-size changes again.

### 2.6 — bfcache staleness fix (request: "only after refreshing... are the distance numbers correct... after refreshing, then a different page, then returning, it's still necessary to refresh")
- Diagnosed as the browser's back-forward cache (bfcache): all page logic ran once as top-level script at initial parse; the "FX SPINE"/"KW SPINE" links reuse a single named tab (`target="fx-kw-spine"`), and navigating back/forward into that tab can restore a frozen pre-bfcache DOM snapshot without re-running script.
- Fix: refactored the tail of the script into a named `update()` function (does group-styling + both distance brackets + empty-note visibbility, now explicitly set in *both* directions — previously only ever turned the empty-note *on*, never back *off*, which was its own latent bug), called once on initial load and again via `window.addEventListener('pageshow', update)` (fires on both normal loads and bfcache restores).
- **Verified with a real click-through simulation, not just a fresh `page.goto()`:** using Playwright's `context.waitForEvent('page')` to capture the actual popup/named-target tab, the test (a) selected pair `{1,2}` on `FX_circle_KW_square.html` and followed "FX SPINE" → correct 1/1; (b) went back, selected quartet `{3,4,63,64}`, followed "FX SPINE" again (reusing the *same* named tab) → correctly updated to 31/11, no stale leftover from the pair; (c) navigated that spine tab away and back (`goBack()`, simulating a bfcache-restorable return) → still correctly showed 31/11, not blank or stale. All three scenarios the user could plausibly have hit are now covered.

## TO-DOS.md and whats-next.md housekeeping (this response and the one before it)

- Added a new top section to `TO-DOS.md`, **"Continue Editing the New FX_KW_spine Page - 2026-08-19 13:49"**, placed at the very top of the file per the user's explicit "top priority" instruction (overriding the `add-to-todos` skill's normal default of appending to the bottom). Full text reproduced verbatim in `<current_todos>` above.
- This document (`whats-next.md`) is that refresh, requested immediately after the TO-DOS addition.

</work_completed>

<work_remaining>

## Immediate — next explicit step per the user's own words

The user said, verbatim, when increasing the panel gap: "this will make space for hexagram display boxes which will be inserted at 'bottom-centre'. but first only increase the gap." That "first" step (2.3 above) is done; **the hexagram display boxes themselves were never built**. This is the literal next task, already captured as the top-priority `TO-DOS.md` entry. No further detail on exactly what these "hexagram display boxes" should contain has been given yet beyond their position ("bottom-centre") — likely analogous to the `#pair-display-fx`/`#pair-display-kw` boxes on `FX_circle_KW_square.html` (which show the selected group's actual hexagram line-glyphs, not just numbers) but this hasn't been confirmed with the user and shouldn't be assumed; ask if unclear when picking this up.

## Uncommitted work needing a decision

1. `diagrams/FX_KW_spine.html` — entirely new, entirely uncommitted, currently mid-build (missing the display boxes above).
2. `diagrams/FX_circle_KW_square.html` — one small 2-line uncommitted diff (the `spine-link-fx`/`spine-link-kw` dynamic href-setting, see `<work_completed>` Phase 1 follow-up). This is a natural, low-risk companion commit alongside the new page (it's the piece that makes the new page reachable with real data), but wasn't explicitly bundled with any commit request this session.
3. `TO-DOS.md` — this session's own new top section, uncommitted.
4. `whats-next.md` — this refresh itself, will be uncommitted at the moment this document is written (standard).

Per this project's standing closing pattern (`feedback_push-reminder` memory), the user should be reminded to consider committing and pushing before ending the session — but note the user has **not asked for a commit this round** (unlike the previous whats-next refresh, which was immediately followed by an explicit "push and commit" request) — don't commit unprompted.

## From TO-DOS.md (verbatim in `<current_todos>` above — this is the complete, current, ordered list)

1. **[Top priority, new this session]** Continue building `diagrams/FX_KW_spine.html` — hexagram display boxes at bottom-centre next.
2. XianTian trigram circle — annotate construction logic (binary/self-reversing vs mixed).
3. Trigram→hexagram concentric-ring diagram (inner 8 trigrams, outer 64 hexagrams).
4. Link the trigram circle + hexagram circle diagrams together.
5. Rebuild the hexagram Group Table from `data/spreadsheets/FX-01.ods` as canonical source.
6. FX/KW trigram circles paired diagram (needs verified King Wen trigram-position data, not assumed from memory).
7. Yin/yang group highlighting for trigrams (depends on item 2).
8. 3D trigram cubes "à la Z.D. Yung" — needs user clarification on the reference/convention.
9. Central-Taiji digram/trigram linking page — needs user clarification on "FX digrams"/"KW digrams".
10. KW square distance-bracket markers ported to the standalone `diagrams/kw-square.html` page specifically (distinct from `FX_circle_KW_square.html`, which already has its own KW-square distance brackets, built in a prior session). **Not checked this session** — verify whether `diagrams/kw-square.html` genuinely still lacks this before assuming it's outstanding, since `TO-DOS.md` has been shown stale before.

</work_remaining>

<attempted_approaches>

- **Row-index-based distance computation** (`maxRowIndex − minRowIndex + 1` from numCirc id suffixes) — tried first for the distance brackets (2.4 above), looked plausible and matched the bracket's own visual vertical extent, but was **wrong by exactly 2×** for every group tested. Root cause: the numCirc id suffix is a spine row-position, not a "paired-row index" — the correct convention (established in `FX_circle_KW_square.html`, used for its own distance brackets and KW-square distance markers) counts in units of *pairs of consecutive hexagram numbers* (via `(n+1)/2`-style halving), not individual hexagram positions. Replaced entirely with `GROUPS[].distance` (FX) / `kwGroupDistance()` (KW), both reused verbatim from the canonical source rather than re-derived — do not reintroduce a row-span heuristic for this if revisiting.
- **`display:none` + `viewBox` auto-crop for non-selected groups** (2.1) — worked exactly as specified at the time, but the user immediately reversed course ("much too empty") once they saw it rendered — the *full* spine context turned out to be wanted, with only the fill state varying. Not a mistake exactly, more a case of the first literal reading of "make a start... only the selected group is shown" needing a follow-up correction once seen. Worth remembering for future "only show X" requests on this page: confirm whether "show" means visibility or visual emphasis before assuming the more drastic (hide-everything-else) interpretation.
- **`npx playwright` (bare)** — from a *prior* session's notes, still relevant: fails with `MODULE_NOT_FOUND` when run as a plain Node script. This session used `npm install playwright-core` in a scratchpad dir + the system's pre-installed `/usr/bin/chromium-browser` (or `/snap/bin/chromium`) passed as `executablePath` — this worked reliably for all ~20+ measurement scripts this session (`measure1.js` through `measure18.js`, `solve.js`, `minitest.js`, `testspine*.js`, `e2e.js`, `darktest.js`, etc., all in the same session-scoped scratchpad `pw/` subdirectory, all now gone in a fresh session but the recipe is worth repeating: `npm install playwright-core`, launch with `executablePath: '/usr/bin/chromium-browser', args: ['--no-sandbox']`).

</attempted_approaches>

<critical_context>

## Where the *previous* (Phase-1-only) version of this handoff went

This `whats-next.md` write **overwrites** the previous one, which had much more granular detail on the Phase-1 `FX_circle_KW_square.html` polish work (exact CSS/JS snippets for the panel-title alignment math, the "150% of one hexagram height = 48px" reference-unit convention, etc.). That work is safely committed (`222af4a`) and pushed, so the loss of blow-by-blow detail is low-risk — but if a future session needs to understand *why* a specific pixel value in that file is what it is, `git log -p -- diagrams/FX_circle_KW_square.html` (or `git show 222af4a`) is the authoritative source, not memory/re-derivation.

## The `FX_KW_spine.html` build pipeline is gone — practical implications for next steps

The generator script (`build_fx_kw_spine.py`) that produced `diagrams/FX_KW_spine.html` lived only in this session's scratchpad and does not persist. This matters for the very next task (hexagram display boxes at bottom-centre):
- **Do not** try to regenerate the whole file from scratch via a new script — that risks losing the now-verified-correct FX/KW spine SVG content and all the fixes from 2.1–2.6.
- **Do** hand-edit `diagrams/FX_KW_spine.html` directly with Edit/Read tools — it's large (~213KB) but is plain, readable HTML/CSS/JS; the huge byte count is almost entirely the two spliced spine `<svg>` blocks (unchanged, verified-correct Inkscape-exported path data), not the parts you'd be touching for new display boxes.
- The file's `<script>` tag (near the bottom) contains, in order: `FX_TO_KW` (64-entry lookup), `GROUPS` (20-entry array, exact copy of `FX_circle_KW_square.html`'s own data), `getSelectedFx()`, `setsEqual()`, `styleCurve()`/`styleGroups()` (fill/dim logic), `svgEl()` (SVG-element helper), `findGroup()`/`kwPairIndexRange()`/`kwGroupDistance()`/`fxGroupDistance()` (distance math), `drawDistanceBracket()`, then the `update()` function and its `pageshow` wiring at the very end. Any new "hexagram display box" logic should likely live inside (or be called from) `update()`, so it participates in the same bfcache-safety re-run behavior established in 2.6 — do not add a second, separately-triggered code path that could reintroduce the staleness bug.

## Naming/positioning conventions established and now load-bearing across both files

- **FX = circle-shaped distance labels; KW = square-shaped distance labels.** Established originally in `FX_circle_KW_square.html`'s `renderPairDistanceBracket(..., shape)` calls, now also followed in `FX_KW_spine.html`'s `drawDistanceBracket(..., shape)`. Keep this convention if adding more distance/shape UI anywhere in this diagram family.
- **`var(--seal)`** is `FX_KW_spine.html`'s equivalent of `FX_circle_KW_square.html`'s `var(--structure)` — same literal color value (`#a23b2e` light / `#e2725a` dark), different variable name because `FX_KW_spine.html`'s palette was copied from `diagrams/spine03/Spine_Page5_Both.html`'s own `:root` block (which predates and is independent of `FX_circle_KW_square.html`'s naming). Don't assume `--structure` exists on the spine page, or `--seal` on the circle/square page.
- **Reserved gutters via padding + absolutely-positioned overlay `<svg>`** is this project's established pattern for side-mounted annotation UI (first used for `FX_circle_KW_square.html`'s `.kw-square-frame`, now reused twice more in `FX_KW_spine.html` for both spine panels). If bottom-centre hexagram display boxes need their own reserved space, consider whether this same pattern (padding-bottom + overlay, or just a plain flex/absolute-positioned `<div>` since display boxes are HTML not SVG-overlay content) is the right fit, or whether something closer to `FX_circle_KW_square.html`'s `#pair-display-fx`/`#pair-display-kw` `<div>`-based boxes (HTML, not SVG) is more appropriate — the latter seems more likely correct since "hexagram display boxes" sounds like it means literal hexagram-glyph boxes like `#pair-display-fx`, not another SVG-overlay annotation.

## Verification methodology (unchanged from before, reconfirmed relevant all session)

`feedback_verification-standard` memory: structural/visual claims need computational proof via actual rendering, not eyeballed code review. Every single change this session (Phase 1 and Phase 2) was verified via a headless-Chromium/Playwright harness before being reported as done — screenshots plus programmatic `getBoundingClientRect()`/`getComputedStyle()`/`getBBox()` assertions. Continue this pattern; the recipe (`npm install playwright-core` + system Chromium `executablePath`) is documented in `<attempted_approaches>` above.

## Persistent-memory context relevant to this project (carried forward, not re-derived this session)

- `feedback_verification-standard`, `feedback_handoff-staleness-check` (confirmed relevant again at this session's start — prior handoff was 5 commits stale), `feedback_whats-next-leads-with-todos` (followed), `project_github-setup` (public repo, Pages auto-deploys `master`), `feedback_push-reminder` (applies once/if a commit happens — not yet requested this round), `project_spine-page-css-gotcha` (same-shape-panel-pair CSS gotcha — directly relevant precedent for the FX-spine/KW-spine panel-alignment work in Phase 1's predecessor session and echoed again in this session's own `.fx-spine-frame`/`.kw-spine-frame` gutter-padding pattern).

</critical_context>

<current_state>

## Git status

```
$ git status --short
 M TO-DOS.md
 M diagrams/FX_circle_KW_square.html
?? diagrams/FX_KW_spine.html
```

- `TO-DOS.md`: this session's new top-priority section added, uncommitted.
- `diagrams/FX_circle_KW_square.html`: 2-line diff (dynamic spine-link hrefs), uncommitted.
- `diagrams/FX_KW_spine.html`: new file, entirely uncommitted, ~213KB.

`origin/master` is at `222af4a` (Phase 1's commit). Nothing from Phase 2 has been pushed.

## Deliverable status

- Phase 1 (`FX_circle_KW_square.html` polish): **complete, committed, pushed.**
- Phase 2 (`FX_KW_spine.html`): **functional and verified for everything built so far** (full-spine display, group highlight, distance brackets with correct numbers, bfcache-safe), but **intentionally incomplete** — the hexagram display boxes at bottom-centre (the whole reason the panel gap was widened) are the explicit next step and have not been started.
- `TO-DOS.md`/`whats-next.md`: housekeeping complete for this round.

## Immediate next step

1. Ask the user (if not already clear from a fresh read of this document) exactly what the bottom-centre hexagram display boxes should contain/look like — likely modeled on `FX_circle_KW_square.html`'s `#pair-display-fx`/`#pair-display-kw` boxes, but not confirmed.
2. Build them directly into `diagrams/FX_KW_spine.html` (hand-edit, not a regenerated pipeline — see `<critical_context>`), wired into the existing `update()` function.
3. Once the user is satisfied with Phase 2, raise committing/pushing — both the new page and the small `FX_circle_KW_square.html` companion diff, plus the `TO-DOS.md` update — but only when asked, per this session's observed pattern of the user driving commit timing explicitly.

</current_state>
