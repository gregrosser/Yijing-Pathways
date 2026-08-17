<reading_instructions>
Whoever reads this document — a fresh Claude instance resuming this work, at the start of a new session — must lead their first response to the user with the contents of <current_todos> below, before summarizing <original_task>, <work_completed>, or anything else in this document.
</reading_instructions>

<current_todos>
# TO-DOS

## KW Body-Schema Numbering - 2026-08-17 11:05

- **Make KW-nums.svg via dvisvgm, place in Inkscape** - Generate the 64 hexagram numbers for the KW (King Wen) body-schema diagram the same way it was done for FX this session, then hand-place them onto `KW-body-schema.svg`. **Problem:** `diagrams/KW-body-schema.svg` is still raw, unprocessed dvisvgm output (confirmed 2026-08-17 — no ring grouping/labeling/numbering applied yet), unlike `diagrams/FX-body-schema-layers-01.svg`, which now has all 20 pair/quartet rings grouped+labeled and all 64 hexagram numbers placed, each grouped with its circle (fill-disc + stroke-ring + digit). **Files:** `diagrams/KW-body-schema.svg` (target), `diagrams/FX-body-schema-layers-01.svg` (reference/precedent for the grouping+numbering structure to replicate), `notes/tools/dvisvgm-howto.md` and `notes/tools/dvisvgm-output-inkscape-edit.md` (the checklist for this exact prep process, written from doing it on FX), `notes/tools/inkscape-howto.md` (Inkscape mechanics notes: Align & Distribute needs ≥2 objects selected for "Relative to: Selection"; layers aren't click-selectable on canvas, use the XML editor or make-active-layer + Ctrl+A). **Solution:** generate `KW-nums.svg` via dvisvgm from a LaTeX source (same method used for `FX_nums.svg`), import into Inkscape as an editable layer (`File → Import`, "Include SVG image as editable object(s)"), then place/center each digit against KW's own n→(cx,cy) position table — that table doesn't exist yet and would need deriving the same way FX's was (parsing the ring paths' bezier endpoints directly, not estimating).

**STATUS UPDATE (this session, 2026-08-17 22:xx): this item is now substantially DONE** — see `<work_completed>` below. `diagrams/KW-body-schema-nums.svg` now exists with all 128 numbers grouped, correctly positioned, and correctly colored, and has been re-embedded into `diagrams/spine02/Spine_Page2_KW.html`. The TO-DOS.md entry above is technically stale (still describes the pre-session state) but has NOT been edited/removed yet this session — do that first when resuming, don't just re-do the work.

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

## FX Num Fill Colour - 2026-08-17 22:39

- **Change FX number-circle fill to `var(--paper)`** - Bring `diagrams/spine02/Spine_Page1_FX.html`'s hexagram number-circle fill in line with the theme-aware fix just applied to the KW page. **Problem:** the FX page's 128 `NumCirc` fill-discs still use hardcoded `fill="#ffffff"` (125+ occurrences), so unlike the KW page they won't follow dark mode — this inconsistency was flagged mid-session and deliberately deferred rather than fixed immediately. **Files:** `diagrams/spine02/Spine_Page1_FX.html` (embedded copy), `diagrams/FX-body-schema-layers-01.svg` (source file, should be fixed there first then re-embedded, mirroring the KW workflow). **Solution:** same as the KW fix this session — change every fill-disc path's `fill="#ffffff"` to `fill="var(--paper)"` in the source SVG, then rebuild the embed (extract the 20 ring elements + 128 NumCirc groups, recolor per the FX line1==line6 gray/black table, splice into the HTML, strip stray `xmlns` declarations). Verify with a before/after screenshot MD5 or visual diff since it should be a zero-layout-change edit.
</current_todos>

<original_task>
Continuation of the KW (King Wen) body-schema numbering work, tracked as the top TO-DOS item from the prior session's handoff: generate the 64 hexagram numbers for the KW body-schema diagram (mirroring the FX body-schema work from the previous session) and hand-place/verify them. The user opened this session already mid-flight, working directly in Inkscape on a new file `diagrams/KW-body-schema-nums.svg`, and asked for help with one specific stuck group (`KW_leftNumCirc_06`). Scope expanded through direct user instruction across the session into: fixing structural bugs found while checking all 128 groups, merging loose fill-discs into their groups, re-embedding the finished diagram into a new spine page (`Spine_Page2_KW.html`), three rounds of fine visual-alignment fixes (horizontal axis, vertical baseline, digit centering within circles), changing the fill color of the number circles to a theme-aware CSS variable, and finally TO-DOS/handoff/git housekeeping.
</original_task>

<work_completed>

## 1. Fixed `KW_leftNumCirc_06` — the user's original stuck point

User reported being unable to get the white fill-disc into this one group in Inkscape. Investigation (coordinate-matching every stroke-ring against every loose fill-disc path in the document) proved the fill-disc for this specific circle **did not exist anywhere in the file** — not loose, not misplaced, genuinely absent (127 of 128 groups had a matching fill disc somewhere; this was the sole exception). Fixed by duplicating the ring's own path geometry into a new `<path fill="#ffffff" id="path305">` (later recolored, see below) as the first child of the group, matching the exact structure of a working group. Verified the group now has exactly 3 children (fill, ring, text) and no duplicate IDs were introduced.

## 2. Full structural audit of all 128 `NumCirc` groups, at user's request ("check this file for all the groups and the associated numbers")

- **Completeness**: found and fixed a second real bug — `KW_rightNumCirc_28` was not a `<g>` at all; its `id`/`inkscape:label` attributes had been mistakenly attached directly to the `<text>` element instead of wrapping a proper group around the fill-disc + ring + text. Fixed by wrapping those three siblings in a real `<g id="KW_rightNumCirc_28" inkscape:label="KW_rightNumCirc_28">`, giving the text a plain `id="text198"` instead.
- **Numbering correctness**: derived and verified (against all 64 rows, zero mismatches) the actual rule the diagram encodes — the right-column number for any row is the **left-column hexagram's FX-native adjacent-pair partner**, translated through the FX↔KW bijection sourced from `diagrams/FX_circle_KW_square.html`'s `data-hex`/`data-kw` cell attributes (`FX_TO_KW`/`KW_TO_FX` maps) and the `GROUPS` JSON embedded in that same file. Cross-checked independently against the source file's own baked-in `inkscape:label="KW{...}"` group labels on the 20 ring elements — matched exactly, which is strong corroborating evidence the derived rule and the file's own structure agree.
- **Duplicates/gaps**: left column = clean straight descending sequence 64→1, no duplicates/gaps. Right column = complete 1–64 once the `_28` bug above was fixed.
- Noted (not fixed, flagged to user): one harmless orphaned white fill-disc, `path283` (d starts `m 286.28564,704.03065`), sits loose inside the numbers layer with no matching ring/text — invisible (white-on-white), left alone.

## 3. Merged all 116 remaining loose fill-discs into their groups (user: "merge all of those into their groups now the way I did for _06")

Matched each loose `<path fill="#ffffff">` sibling to its correct `NumCirc` group by exact coordinate match (first-point of the ring's `d` vs the loose fill's `d`), moved it to be the first child of the group. All 128 groups now contain exactly `[fill, ring, text]`. **Verified zero visual change**: screenshot before/after, MD5-identical PNGs.

## 4. Re-embedded the finished `KW-body-schema-nums.svg` into a new spine page, `diagrams/spine02/Spine_Page2_KW.html`

- Discovered the *existing* `Spine_Page2_KW.html` (and its `spine/` predecessor) was an entirely different, older hand-authored "ribbon" diagram (viewBox `-583.22 -1.00 1218.44 2602.00`), unrelated to the dvisvgm body-schema files — confirmed this by finding `spine/Spine_Page1_FX.html` had originally used the *exact same* old viewBox before last session's FX renovation fully replaced it. This confirmed the correct approach was a **total replacement** of Page 2's SVG content, mirroring exactly what was done to Page 1 last session, not a partial edit.
- Identified the correct 148 elements to extract from `KW-body-schema-nums.svg`: 20 top-level ring/pair elements (`inkscape:label="KW{...}"`) + 128 `NumCirc` groups (which live nested inside a `<g id="g1" inkscape:label="NUMBERS">` wrapper in the source file, unlike FX's equivalent file where they're flat top-level siblings — unwrapped this layer during extraction, i.e. embedded the 128 groups directly, not the wrapping `<g>`).
- Independently cross-verified the 20 ring-group labels' gray/black color assignment: translated the FX-numbered "line1==line6" color table (from the prior session's handoff) into KW numbers via the `FX_TO_KW` bijection, and found the translated set matched the source file's own pre-existing `inkscape:label="KW{...}"` values exactly — used as the color-classification key (10 gray via `var(--ink-faint)`, 10 black via `var(--ink)`, `fill-opacity:0.8`, matching Page 1's established convention).
- Computed a fresh crop `viewBox="163 66 287 660"` for KW's own content bounding box, via `inkscape --query-all` (px@96dpi → native pt units, ÷1.3333, same method as FX), padded ~10 units. Note: `inkscape --export-area`/`--query-*` CLI flags in this Inkscape 1.4.3 build are argument-order-sensitive (options must come *before* the input filename) and reject 3-decimal-place floats in `--export-area` (integers or ≤2 decimals only) — worked around by rounding.
- Added the same page-scoped CSS as Page 1: `.single-panel-wrap--diagram { width: min(1900px, 96vw); }` and `.spine-svg text.f0 { font-family: var(--font-mono); font-size: 5.68px; }`; applied the `single-panel-wrap--diagram` modifier class; updated `aria-label` to "King Wen body schema with hexagram numbers".
- Verified via headless-Chromium screenshot at 1920×2400: numbers legible, gray/black grouping visible, page renders cleanly.

## 5. Fixed a real horizontal-alignment bug found by the user after first embed ("numbers are not vertically aligned… vertical central line of the numbers and… KW symmetric curves must align exactly")

Computed the two axes precisely: the ring/curve geometry's true central x-axis is **exactly 306.6** (baked into the file as a recurring literal — both the `(301.588+311.612)/2` midpoint used by every quartet's two-lobe paths, and the literal start-x of every bare single-path axis-pair). The number circles' actual central axis (computed from 64 left-circle centers, all identically 277.906, and 64 right-circle centers, all identically 289.934 — zero standard deviation each) was **283.92** — which is *exactly* FX's own axis constant (`path55`'s "FX{1,2}" literal start-x in `FX-body-schema-layers-01.svg`). This proved the numbers had been placed using FX's coordinate template and never re-based onto KW's actual (different) ring geometry. Fixed by shifting all 128 `NumCirc` groups (fill, ring, and text `x` coordinates) by `dx = +22.68` in the source file, bringing the number columns to 300.586/312.614 — symmetric around 306.6 exactly. Re-extracted and re-embedded into the spine page; re-verified visually.

## 6. Fixed a vertical-position bug ("numbers… sitting very close but not quite at the correct height… raise the whole double column by ~90% of the diameter of a circle")

Measured the number-circle diameter precisely from the ring path geometry: **8.316** native units. Computed `DELTA_Y = -0.90 × 8.316 = -7.4844` (negative = up, since SVG y increases downward). Applied this uniformly to every `NumCirc` group's fill/ring path `m x,y` start-y and text `y` baseline in the source file (257 paths + 128 texts shifted). Re-extracted/re-embedded/re-verified — numbers now sit snugly against the ribbon's spine rather than floating below it.

## 7. Changed number-circle fill color to a theme-aware variable ("change the fill colour of the circle to the page colour")

Changed all 128 (129 including the harmless stray `path283`) fill-disc paths in the source file from hardcoded `fill="#ffffff"` to `fill="var(--paper)"`. Re-extracted/re-embedded/re-verified. **Noted to user, not yet acted on**: `Spine_Page1_FX.html`/`FX-body-schema-layers-01.svg` still hardcodes `fill="#ffffff"` for its own 125+ number-circle fill-discs — this is now the newest TO-DOS item (see below), deliberately deferred rather than fixed inline.

## 8. Fixed digit-centering-within-circle bugs, in two rounds ("11, 31, 41, 47, 61… can be improved" then "fix 51 and 21… plus a minor one on 14")

- Root-caused via **coordinate analysis, not visual guessing**: computed `circle_cx − text_x` (the horizontal centering offset) for all 128 `NumCirc` groups. For 2-digit numbers this offset clusters tightly (median 3.2433, stdev 0.164) — expected, since the real rendered font is forced monospace via the page's own `.spine-svg text.f0 { font-family: var(--font-mono); ... }` CSS rule (confirmed from Page 1's established CSS, ported to Page 2 in step 4), meaning every 2-digit string should occupy identical width and need an identical centering offset regardless of digit content.
- Found clear outliers: **11, 21, 31, 41, 51, 61** (offset ≈ 2.69–2.89, all ~0.35–0.55 below median — all share a trailing "1", suggesting the person hand-centering by eye was visually biased by the narrow "1" glyph) plus a smaller outlier on **14** (+0.20). **47** was *not* a statistical outlier (offset 3.169 vs median 3.243, well within normal spread) but the user asked for it anyway — included in the first fix batch regardless, since a uniform median-based correction cannot make an already-close value worse.
- Fixed by setting `text/@x = circle_cx − 3.2433` (the population median) for both left/right instances of each flagged number, first for `{11, 31, 41, 47, 61}`, then for `{51, 21, 14}` in a follow-up round.
- **Verification method** (developed specifically for this step, notable for future reuse): rendering the bare source SVG directly in a browser does **not** show the number circles' true colors/fonts correctly, because their `fill`/`stroke` use CSS custom properties (`var(--paper)`, `var(--ink)`, etc.) that are only defined in the *page's* `:root` stylesheet, not inside the standalone SVG file itself — loading the raw `.svg` directly gives invisible/wrong-colored circles. Built a minimal HTML harness (`:root { --paper:...; --ink:...; }` + inlined extracted SVG content + the real `text.f0` monospace CSS rule) to get an accurate zoomed render, screenshotted at `--window-size` set to an exact multiple of the SVG's native viewBox (giving an exact, verified px-per-unit scale factor, e.g. k=10.0), then cropped ±6–8 native units around each target circle's computed center using PIL, montaged into a labeled grid with a red crosshair marking the computed circle center, and visually confirmed each digit sits centered on its crosshair. This is the only reliable way found this session to visually spot-check small-scale detail, since (a) Inkscape's CLI `--export-area`/`--query-*` flags are unreliable/quirky for this (see Attempted Approaches), and (b) the real spine page's responsive CSS makes precise pixel↔native-unit mapping hard to compute directly.

## 9. TO-DOS.md maintenance

Added a new item, **appended to the bottom** of `TO-DOS.md` (default `add-to-todos` behavior — no override requested this time, unlike the previous session's top-of-list request): "FX Num Fill Colour" — port the `var(--paper)` fill-color fix (step 7 above) to the FX page/source file too. Full item text preserved verbatim in `<current_todos>` above. **Not yet done**: the pre-existing "KW Body-Schema Numbering" TO-DOS item at the top of the list is now stale (describes work that is largely complete per steps 1–8 above) but has not been edited or removed — flagged in `<current_todos>` with a status update note, and left as the first actionable item for whoever resumes.

## 10. This document (`whats-next.md`) regenerated per explicit user request

Per user's exact instruction ("refresh the to-do list and add: FX num fill colour to 'page' then refresh the whats-next and 'push to master'"), this handoff was regenerated to capture the full session. Git commit + push to `origin/master` is the next and final step (see `<current_state>` — not yet done as of this writing, is the immediate next action).

</work_completed>

<work_remaining>

## Immediate — this session's own wrap-up (in progress as this document is written)

1. **Commit and push to `origin/master`** — explicitly requested by the user as the last step of this session, not yet executed. Working tree currently has: `TO-DOS.md` (modified, new bottom item), `diagrams/KW-body-schema.svg` (modified — see Critical Context below, this is *not* Claude's edit), `diagrams/spine02/Spine_Page2_KW.html` (modified, full renovation), `whats-next.md` (this file, modified), plus three new untracked files: `diagrams/FX_nums.svg`, `diagrams/KW-body-schema-nums.svg`, `diagrams/KW-nums.svg`. All of this should be staged and committed together (it's all one coherent unit of work from this session), then pushed.

## From TO-DOS.md (see `<current_todos>` above for full detail)

1. **Update the stale "KW Body-Schema Numbering" TO-DOS entry** — it currently describes the *pre-session* state (numbering "not yet done"); the work is now done (modulo the note in step 1 below). Either mark it complete/remove it, or rewrite it to reflect only what's genuinely still open (see next point).
2. **`diagrams/KW-body-schema.svg` vs `diagrams/KW-body-schema-nums.svg`** — clarify/resolve the relationship between these two files (see Critical Context — this was *not* investigated deeply this session, just observed as a modified-but-untouched-by-Claude file in `git status`). It's possible `KW-body-schema.svg` (the ring-only master, analogous to `FX-body-schema.svg`) needs to be reconciled with or updated from `KW-body-schema-nums.svg` (the numbered working file, analogous to `FX-body-schema-layers-01.svg`), the same two-file relationship FX has. Not yet confirmed with the user.
3. **FX Num Fill Colour** (new item, full detail in `<current_todos>`) — apply the same `fill="var(--paper)"` fix to `Spine_Page1_FX.html`/`FX-body-schema-layers-01.svg` that was applied to KW this session.
4. XianTian trigram circle construction-logic annotation.
5. Trigram→hexagram concentric-ring diagram.
6. Link trigram circle + hexagram circle diagrams.
7. Rebuild Group Table from a spreadsheet source (`data/spreadsheets/FX-01.ods`).
8. FX/KW trigram circles paired diagram.
9. Yin/yang group highlighting for trigrams.
10. 3D trigram cubes ("à la Z.D. Yung" — needs user clarification).
11. Central-Taiji digram/trigram linking page (needs clarification).
12. KW square distance-bracket markers.

## Not yet asked / open judgment calls

- Whether `Spine_Page2_KW.html`'s dark-mode rendering has been verified in a real browser — same open gap noted for `Spine_Page1_FX.html` in the previous session's handoff (headless-Chromium in this environment can't reliably emulate `prefers-color-scheme`; Playwright MCP confirmed broken). Not re-checked this session.
- Whether the harmless orphaned `path283` stray fill-disc (step 2 above) should be deleted for cleanliness — flagged, not acted on.

</work_remaining>

<attempted_approaches>

- **`inkscape --query-all`/`--export-area` CLI quirks** — this Inkscape 1.4.3 build requires options to precede the input filename (`inkscape --export-area=... file.svg`, not `inkscape file.svg --export-area=...` — the latter silently does nothing, exit 0, no error, no output file). Also rejects `--export-area` values with 3 decimal places ("Cannot parse export area") — 2 decimals or integers only. Cost significant time before being diagnosed; worth remembering for next time this tool is needed.
- **Rendering the bare/standalone `KW-body-schema-nums.svg` directly in a browser to visually verify anything about the number circles** — doesn't work, because the file's `fill`/`stroke` values are CSS custom properties (`var(--paper)`, `var(--ink)`, `var(--ink-faint)`) with no `:root` definitions inside the SVG document itself; a standalone render shows the circles with unresolved/invisible paint. Worked around by building a minimal HTML harness with the `:root` variables and the real `text.f0` CSS rule copied in, and inlining the extracted SVG content into that harness for rendering — this is now the established method for any future zoomed visual check of this content.
- **Assuming a fixed/coincidental pixel-per-unit scale factor when screenshotting** (e.g. guessing k=4 or k=8 from an arbitrary `--window-size` choice) — wrong; a bare SVG document loaded via `file://` renders at its own *intrinsic* size (native pt-to-px conversion, ~1.333×) in the top-left of an oversized window, not stretched to fill it. The reliable method: set the outer `<svg>` element's own `width`/`height` attributes to an exact round multiple of its `viewBox` (e.g. `width="5950" height="8420"` for a `0 0 595 842` viewBox → exactly k=10), then set `--window-size` to match those exact pixel dimensions.
- **Guessing which numbers needed digit-centering fixes from theory alone** (e.g. assuming glyph-width-based centering using the LaTeX/dvisvgm font's actual glyph metrics via `inkscape --query-width` on the text elements) — actively misleading: the *displayed* font is monospace (CSS override), not the original LaTeX glyphs, so LaTeX-glyph-width-based "ideal" centering doesn't match what's actually rendered. The correct method was purely statistical/coordinate-based (median offset across all same-length numbers), not font-metric-based.
- **`bc`/`printf "%.0f"` in a bash loop for rounding coordinates** — hit shell locale/floating-point quirks (`printf: invalid number` on plain decimal strings from `bc` output) that wasted a couple of iterations; switched to doing all coordinate math in Python instead, which was more reliable throughout this session generally.

</attempted_approaches>

<critical_context>

## The FX↔KW bijection and group data — where it lives, reused repeatedly this session

`diagrams/FX_circle_KW_square.html` contains, embedded in a `<script>` block:
- `HEXLINES` — FX-numbered hexagram → 6-line yin/yang array.
- `GROUPS` — the 20 "line1==line6" groups (8 pairs + 12 quartets) in FX numbering, each with `members` and (for quartets) `pairs` (the FX-native complement/cuo sub-pairing).
- The FX↔KW bijection itself is **not** hardcoded as a JS object literal — it's derived at page-load time from `data-hex="N" data-kw="M"` attributes on `.cell[data-hex]` elements elsewhere in that same file (a King Wen square grid). To reuse this bijection outside a browser (as done repeatedly this session via Python/lxml), regex-extract these attribute pairs directly: `re.findall(r'data-hex="(\d+)" data-kw="(\d+)"', html)`.

## The verified numbering rule for `KW-body-schema-nums.svg` (load-bearing, don't re-derive from scratch — re-verify against this)

For any row, `right_number = FX_TO_KW[ partner_fx( KW_TO_FX[left_number] ) ]`, where `partner_fx(m) = m+1` if `m` is odd, else `m-1` (i.e., the KW number's *native FX-numbering* adjacent-pair partner, translated back into KW numbers). Verified exactly against all 64 rows, zero exceptions, including cross-checking the one structurally-broken row (`_28`) whose digit value was already correct despite the group-wrapping bug.

## Exact geometric constants for `KW-body-schema-nums.svg` (all as of the *end* of this session, i.e. post all fixes — don't reuse pre-fix values)

- Ring/curve geometry's central x-axis: **306.6** (native units).
- Number-circle diameter: **8.316** (native units); radius 4.158.
- Left-column circle centers: **x = 300.586** (constant across all 64, zero stdev).
- Right-column circle centers: **x = 312.614** (constant across all 64, zero stdev).
- Vertical baseline-to-circle-center offset: **y ≈ +2.03** (text `y` attribute minus circle center `y`; near-constant, this is the digit's font baseline sitting below center, unaffected by any of this session's edits since the y-shift in step 6 was applied uniformly).
- Median 2-digit horizontal centering offset (`circle_cx − text_x`): **3.2433** — the value now applied to all corrected outlier numbers (11, 21, 31, 41, 47, 51, 61, 14).
- Content bounding box (148 kept elements: 20 rings + 128 NumCirc): `x:[173.291,439.910]` `y:[76.247,716.454]` in native pt units — **unchanged by any of the x/y number-shifting fixes**, because the wide ribbon curves (not the small number circles) dominate the bbox in both axes. Embedded `viewBox="163 66 287 660"` (bbox + ~10 padding) remains correct; no need to recompute unless the ring/curve geometry itself is edited.

## Full 20-group gray/black KW-numbered color table (translated from the FX table via the bijection, cross-verified against the source file's own `inkscape:label` values — exact match)

**Gray** (`var(--ink-faint)`): `KW{1,2}`, `KW{61,62}`, `KW{29,30}`, `KW{27,28}`, `KW{7,8,13,14}`, `KW{9,10,15,16}`, `KW{25,26,45,46}`, `KW{37,38,39,40}`, `KW{31,32,41,42}`, `KW{21,22,47,48}`

**Black** (`var(--ink)`): `KW{11,12}`, `KW{53,54}`, `KW{63,64}`, `KW{17,18}`, `KW{23,24,43,44}`, `KW{19,20,33,34}`, `KW{5,6,35,36}`, `KW{51,52,57,58}`, `KW{55,56,59,60}`, `KW{3,4,49,50}`

## The extraction/re-embed pipeline (repeated ~5 times this session — this is now the established, reusable procedure for `Spine_Page2_KW.html`)

1. Parse `diagrams/KW-body-schema-nums.svg` with lxml.
2. Collect the 20 top-level elements whose `inkscape:label` starts with `"KW{"` — these are the ring/pair curves. Recolor each (and every descendant `<path>`) per the gray/black table above: set both the `fill`/`stroke` XML attributes *and* the `style` attribute's `fill`/`stroke`/`stroke-opacity`/`fill-opacity`/`stroke-dasharray` keys, matching Page 1's established convention (both places set redundantly, for safety).
3. Collect the 128 `<g>` children of `g1` (`id="g1"`, `inkscape:label="NUMBERS"`) — these are the `NumCirc` groups. Do **not** include `g1` itself, and do **not** include its one stray loose `path283` child.
4. Serialize each kept element via `etree.tostring()`, then strip auto-injected `xmlns`/`xmlns:*` declarations via `re.sub(r'\s+xmlns(:\w+)?="[^"]*"', '', s)` (lxml injects these on every fragment; they're not needed once spliced into the already-namespaced host HTML).
5. Join and splice into `Spine_Page2_KW.html`, replacing everything between the known-fixed opening `<svg class="spine-svg" viewBox="163 66 287 660" ...>` tag and the closing `</svg>` (regex with `re.DOTALL`, exactly 1 match asserted).
6. Screenshot-verify (see harness method below) after every change to this pipeline's *inputs* (i.e. after any edit to the source `.svg` file) — never trust an edit without re-rendering.

## Screenshot/verification harness (see also Attempted Approaches)

For zoomed pixel-level inspection of small features (digit centering, etc.):
```html
<style>
:root { --paper:#f2ecdc; --ink:#201d16; --ink-faint:#b8ae96; }
body { margin:0; background:var(--paper); }
svg { display:block; }
text.f0 { font-family: ui-monospace, "SF Mono", Menlo, Consolas, monospace; font-size: 5.68px; }
</style>
<svg xmlns="http://www.w3.org/2000/svg" width="5950" height="8420" viewBox="0 0 595 842">
<!-- inline the extracted 148-element content here -->
</svg>
```
Screenshot with `chromium-browser --headless --disable-gpu --no-sandbox --screenshot=out.png --window-size=5950,8420 file://<path>` — gives an exact k=10.0 px-per-native-unit scale (since 5950/595=8420/842=10 exactly), safe to compute crop boxes directly as `(cx±N)*10`. Must write the harness HTML to `$HOME` or similar — nested scratchpad paths fail for Chromium reads/writes (per the standing environment note from the previous session, reconfirmed).

## Environment notes reconfirmed/extended this session

- `chromium-browser --headless --disable-gpu --no-sandbox --screenshot=<path> --window-size=<W>,<H> file://<absolute-path>` remains the working screenshot command; scratchpad paths still fail, use `$HOME`.
- `inkscape --query-all <file>` (options before filename) still works and remains the way to bulk-query every element's `x,y,width,height` in px@96dpi.
- Playwright MCP still confirmed non-functional in this environment (not re-tested this session, carried forward as known-broken from previous session's notes).
- `montage`/`convert` (ImageMagick) are available but `montage` had a mysterious path-resolution failure this session (`unable to open image ... No such file or directory` on files that `ls` confirmed existed) — root cause not diagnosed (possibly a snap-confinement quirk similar to Chromium's, not investigated further); worked around by using Python/PIL for all image compositing instead, which worked reliably throughout.

## User's demonstrated preferences (this session, worth carrying forward)

- Extremely precise, spatial/geometric feedback style — gives exact quantitative corrections when possible (e.g. "raise by approximately 90% of the diameter of a circle") rather than vague "move it up a bit." When given a request like this, compute the referenced quantity exactly from the file (don't estimate) and apply it exactly.
- Notices small visual misalignments others might not (sub-unit centering errors, axis misalignment) — this project's whole standing preference for "exact computed/verified answers over eyeballing" (from persistent memory) extends to the user's own visual QA process, not just Claude's. Expect further rounds of this kind of fine-detail correction request on other diagrams.
- Comfortable giving terse, elliptical instructions ("fix 51 and 21 (both sides), plus a minor one on 14") that assume Claude already has the relevant context loaded (in this case, from Claude's own immediately-preceding offer to fix those specific numbers) — reads as trust that context carries forward correctly within a session; a fresh/resumed session would need to rebuild that same context from this document before such a terse instruction would be actionable.
- Explicit two-step session-end pattern: "refresh the to-do list and add: X, then refresh the whats-next, and 'push to master'" — i.e. TO-DOS update → handoff regeneration → git push, in that specific order, as the standard closing ritual for a work session in this project.

</critical_context>

<current_state>

## Git — NOT yet committed or pushed (this is the immediate next action)

Working tree as of this document's writing:
```
 M TO-DOS.md
 M diagrams/KW-body-schema.svg
 M diagrams/spine02/Spine_Page2_KW.html
 M whats-next.md
?? diagrams/FX_nums.svg
?? diagrams/KW-body-schema-nums.svg
?? diagrams/KW-nums.svg
```
Local `master` is at `39acd98` (same as `origin/master` — no prior unpushed commits carried in from before this session). All of the above should be staged, committed as one coherent unit (this session's KW body-schema numbering work + housekeeping), and pushed to `origin/master`.

**Note on `diagrams/KW-body-schema.svg`**: this file shows as modified in `git status`, but Claude did not edit it this session — all of Claude's edits targeted `diagrams/KW-body-schema-nums.svg` (a separate, untracked file). The diff (737 lines changed) includes Inkscape view-state metadata changes (`inkscape:zoom`, `inkscape:cx/cy`) and what looks like the removal of a loose `path17` element plus grouping changes — consistent with the user's own parallel hand-editing work in Inkscape on the *original* ring-only master file, separate from the `-nums.svg` copy Claude was working on. This was not investigated in depth; flagged as a `<work_remaining>` item to clarify the intended relationship between the two files before assuming either is "more correct" than the other.

## Files — `diagrams/` (KW body-schema work)

- `KW-body-schema-nums.svg` — **new, untracked**. The canonical numbered/grouped working file (analogous to `FX-body-schema-layers-01.svg`). All 128 `NumCirc` groups complete (fill+ring+text), correctly positioned (both axes fixed), correctly colored, digit-centering fixed for 8 numbers. This is the current source of truth for the KW body-schema numbering.
- `KW-body-schema.svg` — **modified** (by the user, in parallel, per above) — ring-only master file, not touched by Claude this session.
- `KW-nums.svg` — **new, untracked**. Presumably the dvisvgm-generated raw digit glyphs (the KW analog of `FX_nums.svg`), source material for building `-nums.svg`; existence noted, contents not inspected this session.
- `FX_nums.svg` — **new, untracked**. Not touched or inspected this session; presumably left over from the previous session's FX numbering work and only now appearing in `git status` (possibly just never staged before).
- `spine02/Spine_Page2_KW.html` — **modified**, fully renovated this session: old ribbon-diagram content entirely replaced with the finished KW body-schema (148 elements), all alignment/color fixes applied, verified via multiple rounds of screenshot inspection.

## Files — top level

- `TO-DOS.md` — modified, new "FX Num Fill Colour" item appended at bottom; pre-existing "KW Body-Schema Numbering" item at top is stale (see `<work_remaining>`).
- `whats-next.md` (this file) — being regenerated right now per explicit user request, immediately before the git commit+push step.

## Immediate next step

Stage all changed/new files listed above, write a commit message covering this session's KW body-schema numbering + spine-page-2 renovation + digit-alignment fixes + TO-DOS update, commit, and push to `origin/master`. This was the explicit final instruction of the session ("push to master") and has not yet been executed as of this document being written.

</current_state>
