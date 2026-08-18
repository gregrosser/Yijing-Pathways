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

## Spine03: Fork the Spine Series for Same-Diagram eq/neq Comparison Pages - 2026-08-18 10:55

- **Copy `diagrams/spine02/` to a new `diagrams/spine03/` and continue editing there** - Fork the just-completed 10-page spine series into a new `spine03` directory; all further spine-page editing continues on the `spine03` copy, not `spine02`. **Problem:** `spine02`'s 10 pages are considered complete/frozen for now (per explicit instruction at the end of the prior session); the next round of variant pages should not disturb that finished set. **Files:** `diagrams/spine02/*` (source, all 10 `Spine_Page*.html` files plus any other contents of the directory) → `diagrams/spine03/*` (new copy, same filenames). **Solution:** straight recursive copy of the directory; update internal nav `href`s only if/as needed once the new pages below change the page count or ordering — check whether the existing 1↔10 nav loop still makes sense once spine03 diverges, or whether it needs its own numbering.

- **Build an FX-only eq/neq comparison page (no numbers)** - New page showing the FX `line 1 == line 6` groups next to the FX `line 1 ≠ line 6` groups, side by side on the same page, with no hexagram numbers. **Problem:** the existing spine02 pages only ever pair FX-with-KW (Pages 3/8) or show one diagram's eq-only or neq-only groups alone (Pages 4/5/9/10) — no page puts FX's own eq and neq subsets directly next to each other for comparison. **Files:** new page in `diagrams/spine03/` (naming TBD, e.g. `Spine_PageXX_FX_EqVsNeq.html`); reuse the `diagrams/FX-body-schema-layers-01.svg` source and the `FX_EQ` group-label set established in the prior session's extraction pipeline (see that session's `whats-next.md` for the exact set and the recolor/extraction approach — the pipeline script itself was only ever scratchpad-local and no longer exists, but the logic and constants are documented there). **Solution:** two-panel layout (left = FX eq groups only, right = FX neq groups only, both same diagram/source, no number circles on either side) — likely the closest existing template is the two-panel CSS scaffold built for spine02 Pages 4/5/9/10, adapted to put FX twice instead of FX+KW.

- **Build a KW-only eq/neq comparison page (no numbers)** - Same as the item above, but for KW instead of FX: KW `line 1 == line 6` groups next to KW `line 1 ≠ line 6` groups, side by side, no numbers. **Files:** new page in `diagrams/spine03/`; `diagrams/KW-body-schema-nums.svg` source and the `KW_EQ` group-label set (same prior-session reference). **Solution:** same two-panel approach as the FX page above, KW content on both sides instead of FX.
</current_todos>

<original_task>
This session opened with the user asking to read `whats-next.md` (the handoff from the prior session). The only substantive task given afterward was: "the 'spine ribbons diagrams' listed in the index.html should link to /home/greg/pCloudDrive/YIJING/Yijing-Pathways/diagrams/spine02/" — i.e. repoint the "Spine-Ribbon Diagrams" entry in `index.html`'s Structure strand from the old `diagrams/spine/` directory to the current, completed `diagrams/spine02/` series. The user then asked to "refresh whats-next" (this document).
</original_task>

<work_completed>

## 1. Read and reported on the prior handoff (`whats-next.md` as it existed at session start)

Led the response with the prior session's `<current_todos>` block (the same 6 TO-DOS sections now reproduced verbatim in `<current_todos>` above, at that time *not yet* including the new "Spine03" section — see Item 3 below for why that section's presence is a surprise this session did not create).

**Staleness finding:** the prior `whats-next.md`'s own `<current_state>` claimed `TO-DOS.md` and `whats-next.md` were the only uncommitted files, with a commit+push as the very next step. Checking `git log` showed that commit had in fact already happened (`420e8bd`, "Clean up TO-DOS now the spine pages are complete, refresh whats-next") — the prior handoff document was stale by one commit at the moment this session started reading it. This confirms the project's standing "handoff documents can lag actual repo state — check `git log`/`git status`, don't trust the doc blindly" pattern.

## 2. Fixed the "Spine-Ribbon Diagrams" link in `index.html` (the session's actual task)

- Located the link via `grep -n -i "spine" index.html` → found it at what was then line 316: `<a class="entry flagship" href="diagrams/spine/Spine_Page1_FX.html" ...>` inside the "Structure" strand's entries list (`entry-title` = "Spine-Ribbon Diagrams", `entry-desc` mentions "A 10-page full-SVG series... Click-to-select a single ribbon is the next feature planned for this series.").
- Confirmed both `diagrams/spine/` (old) and `diagrams/spine02/` (current, completed per the prior session) contain the same 10 `Spine_PageN_*.html` filenames (`spine02` additionally has one stray extra file, `Spine_Page1_FX-nums-noFill.html`, already flagged as an unaddressed leftover in the prior handoff — not touched this session).
- Edited `index.html` line 316: `href="diagrams/spine/Spine_Page1_FX.html"` → `href="diagrams/spine02/Spine_Page1_FX.html"`. This is the only line changed in the file.
- Verified the fix is sufficient on its own: checked each spine02 page's internal prev/next navigation links (`grep -n "Spine_Page" diagrams/spine02/Spine_Page1_FX.html` → `prev-link href="Spine_Page10_Line1ne6.html"`, `next-link href="Spine_Page2_KW.html"`) and confirmed they use bare relative filenames (no `diagrams/spine/...` prefix baked in), so once the entry-point link lands the reader in `spine02/`, the full 1→2→…→10→1 nav loop stays inside `spine02/` automatically — no further link changes were needed anywhere in the 10 spine pages themselves.

## 3. Discovered a new, pre-existing uncommitted addition to `TO-DOS.md` not created by this session

While diffing `TO-DOS.md` against `HEAD` (`git diff TO-DOS.md`) to check current state before writing this handoff, found a new section already present in the working tree, dated **2026-08-18 10:55** (today's date, but not added by any action in this session's own transcript): **"Spine03: Fork the Spine Series for Same-Diagram eq/neq Comparison Pages"**, containing 3 new items:
- Copy `diagrams/spine02/` → new `diagrams/spine03/`, continue all further spine editing there (keep `spine02` frozen/complete).
- Build an FX-only eq/neq comparison page (FX eq groups next to FX neq groups, same diagram, no numbers) in `spine03`.
- Build a KW-only eq/neq comparison page (same idea, KW instead of FX) in `spine03`.

This addition's provenance is unknown to this session — it was not typed, discussed, or acted on in this conversation's own transcript. It is included verbatim in `<current_todos>` above per this document's standing "reproduce `TO-DOS.md` verbatim, don't summarize" instruction, and is called out explicitly here so the next reader doesn't mistake it for something this session did or fully understood the origin of.

</work_completed>

<work_remaining>

## Immediate — this session's own wrap-up

1. **Commit and push `index.html`** (the spine-ribbons link fix) — not yet done. `git status --short` currently shows:
   ```
    M TO-DOS.md
    M index.html
   ```
   `index.html`'s change is this session's own completed work and should be committed. `TO-DOS.md`'s change (the new Spine03 section, see Item 3 above) is *not* this session's own edit but is sitting in the same working tree — worth confirming with the user whether they want it committed together, separately, or reviewed first, since its origin is unclear to this session.
2. **Refresh of `whats-next.md`** — in progress as this document is written; this is that refresh.
3. Standard closing pattern for this project (per persistent memory: `feedback_push-reminder`) — remind the user to consider `git push` to master before ending the session, once whatever commit(s) are made.

## From TO-DOS.md (see `<current_todos>` above for full detail — this is the complete, current list)

1. Reconcile `diagrams/KW-body-schema.svg` with `diagrams/KW-body-schema-nums.svg`.
2. XianTian trigram circle — annotate construction logic (binary/self-reversing vs mixed).
3. Trigram→hexagram concentric-ring diagram (inner 8 trigrams, outer 64 hexagrams).
4. Link the trigram circle + hexagram circle diagrams together.
5. Rebuild the hexagram Group Table from `data/spreadsheets/FX-01.ods` as canonical source.
6. FX/KW trigram circles paired diagram (needs verified King Wen trigram-position data, not assumed from memory).
7. Yin/yang group highlighting for trigrams (depends on item 2 being resolved first).
8. 3D trigram cubes "à la Z.D. Yung" — **needs user clarification** on the reference/convention before starting.
9. Central-Taiji digram/trigram linking page — **needs user clarification** on what "FX digrams" vs "KW digrams" means.
10. KW square distance-bracket markers (straight-line/tick version of the FX circle's arc distance markers).
11. **Spine03 fork + FX-only/KW-only eq-vs-neq comparison pages** (new section, provenance unconfirmed — see Item 3 in `<work_completed>`). Recommend confirming with the user this session's addition is intentional/wanted before starting it, given its unexplained appearance.

## Not yet asked / open judgment calls

- Whether the new "Spine03" TO-DOS section (Item 3 in `<work_completed>`) was deliberately added by the user through some channel outside this conversation (e.g. hand-edited the file directly, or a separate/parallel session), or is stray/unintended content. Worth a direct check-in before treating it as an actionable to-do.
- The stray leftover file `diagrams/spine02/Spine_Page1_FX-nums-noFill.html` (flagged in the prior two handoffs as an intermediate/duplicate artifact not part of the canonical 10-page nav chain) still exists and remains untouched.
- Whether the 10 spine02 pages' dark-mode rendering has ever been verified in a real browser — still not checked, per the prior handoff (headless-Chromium in this environment can't reliably emulate `prefers-color-scheme`; Playwright MCP was confirmed non-functional in a prior session).
- The reusable Python spine-page extraction/build pipeline from the prior session (`extract.py`, `build_pages.py`) was scratchpad-only and is now gone (scratchpad is session-scoped). If `spine03` work proceeds, this pipeline will need to be reconstructed — the prior session's `whats-next.md` documented the exact logic/constants needed to do so, but that document has now been overwritten by this one. **The reconstruction details (recolor precedence rule, `FX_EQ`/`KW_EQ` label sets, sizing-formula constants, CSS templates) lived only in the *previous* `whats-next.md` version and are not reproduced in full here** — if `spine03` work starts, check `git log -p -- whats-next.md` or the prior session's transcript for that detail rather than re-deriving from scratch, since it was hard-won (multiple false starts) the first time.

</work_remaining>

<attempted_approaches>

No new approaches were tried or failed this session — the `index.html` link fix was a single, direct, successful edit (grep to locate, read surrounding context, edit, verify via internal nav-link inspection). No dead ends this session.

</attempted_approaches>

<critical_context>

## The `index.html` "Structure" strand entries — relevant surrounding structure

The "Spine-Ribbon Diagrams" entry (now fixed) sits inside `index.html`'s `<div class="spine">` → first `<section class="strand" data-strand>` (accent `var(--structure)`) → `<div class="entries">`, alongside sibling entries for: FX↔KW Correspondence (`diagrams/FX_circle_KW_square.html`), Group Table Properties (`diagrams/group-table.html`), King Wen Square (`diagrams/kw-square.html`), Spinal Mapping note, Group Table Observations note, FX→KW Correspondence & Verification note, a Structural Body Schemas PDF entry, and FuXi Circle (`diagrams/FuXi21.html`). None of these siblings were touched this session — only the one `href` on the flagship Spine-Ribbon entry.

## `diagrams/spine/` vs `diagrams/spine02/`

- `diagrams/spine/` — the **old** 10-page series (pre-rebuild), still present on disk, now orphaned from `index.html` (nothing links to it anymore after this session's fix). Not deleted — left in place; deletion was not requested and wasn't considered, since the prior session's rebuild work explicitially preserved it as a comparison/backup reference (`diff`/`md5sum` against it was how the old page structure was originally understood).
- `diagrams/spine02/` — the **current, completed, 10-page rebuilt series** (per the prior session's extensive work: matched diagram scale, matched nav-button position, correct per-panel captions, correct eq/neq group filtering, correct gray/black coloring, correct complementary-pair fill/stroke-width styling — all explicitly confirmed complete by the user before this session began). This is now correctly the link target from `index.html`.
- Both directories currently contain the identical set of 10 `Spine_PageN_*.html` filenames (`spine02` has one extra stray file, see below) — this identical naming is *why* only the single entry-point `href` in `index.html` needed changing; every page's own internal prev/next nav uses bare relative filenames with no directory prefix, so they resolve correctly within whichever directory the browser is currently in.

## The unexplained new TO-DOS section

Flagged prominently in `<work_completed>` Item 3 and `<work_remaining>` — this session found `TO-DOS.md` already modified with a new "Spine03" section at session start, dated with today's date/time (2026-08-18 10:55) but not written by any action visible in this conversation's transcript. Treat this as **unverified/unconfirmed** content — real possibility it was added by the user directly (e.g. hand-typed into the file, or via a different/parallel Claude session not visible here) and is fully intentional, but this session has no way to confirm that. Flag it to the user rather than silently either acting on it or dropping it.

## Persistent-memory context relevant to this project (carried forward, not re-derived this session)

- `feedback_verification-standard`: structural claims need exhaustive computational proof, not eyeballing — applied loosely in the link-fix work (verified nav hrefs via grep rather than assuming).
- `feedback_handoff-staleness-check`: `whats-next.md` can lag actual repo state; check file mtimes/git log on resume — directly confirmed relevant again this session (see Item 1 above).
- `project_github-setup`: public repo, GitHub Pages live at `gregrosser.github.io/Yijing-Pathways`, pushes to `master` auto-deploy — relevant once `index.html` is pushed, the live site's Spine-Ribbon Diagrams link will start pointing at `spine02/`.
- `feedback_push-reminder`: remind the user to consider `git push` to master before ending a Yijing Pathways session — applies at the end of this session once commits are made.
- `feedback_whats-next-leads-with-todos`: lead first response with the to-do list when reading `whats-next.md` at session start — followed at the start of this session.
- `project_asana-removed`: TO-DOS.md is the sole tracker (Asana deactivated) — relevant background for why the unexplained new TO-DOS section (Item 3) can't have come from an Asana sync; it must be a direct file edit or a separate Claude session.

</critical_context>

<current_state>

## Git — one small fix ready to commit, plus an unrelated pre-existing uncommitted change

```
$ git status --short
 M TO-DOS.md
 M index.html
```

- `index.html`: **this session's completed work** — the single-line `href` fix (`diagrams/spine/` → `diagrams/spine02/`) on the "Spine-Ribbon Diagrams" entry. Ready to commit.
- `TO-DOS.md`: **not this session's edit** — contains the new "Spine03" section (see `<critical_context>` above) whose origin is unconfirmed. Sitting in the working tree already at session start, before any action in this transcript. Whether/how to commit this is an open question for the user, not yet decided.

`origin/master` is at `420e8bd` ("Clean up TO-DOS now the spine pages are complete, refresh whats-next"). Nothing has been pushed this session.

## Deliverable status

The `index.html` link fix is **complete and correct** but **not yet committed or pushed**. No other work was requested or performed this session.

## Immediate next step

1. Ask the user (or otherwise confirm) whether the uncommitted `TO-DOS.md` "Spine03" addition is intentional and should be committed alongside `index.html`, or handled separately.
2. Commit `index.html` (and `TO-DOS.md` if confirmed) with a clear message.
3. Push to `origin/master` — per the project's standing closing pattern, remind the user of this if they don't raise it first.

</current_state>
