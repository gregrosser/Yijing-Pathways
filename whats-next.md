<original_task>
Continuation of the `diagrams/spine/` → `spine02/` nested-ellipse-style renovation pilot (superseded prior-session context). This session picked up mid-flight from a paused handoff where: all 64 hexagram numbers had *supposedly* just been hand-placed in Inkscape but never verified, and re-embedding into `Spine_Page1_FX.html` was the next unstarted step. The session's actual arc, driven by direct user instruction as it evolved:
1. Verify the true on-disk state of the multiple candidate body-schema SVG files left over from the prior session (the handoff explicitly flagged this as unresolved/unconfirmed).
2. Fix a structural grouping gap found during that verification (fill-discs and digit text not actually bundled with their circles).
3. Re-embed the finished ring+number geometry into `diagrams/spine02/Spine_Page1_FX.html`, replacing the numbers-free embed left from the prior session.
4. Iteratively fix display-scale/legibility problems in the embedded page (viewBox crop, container width) — driven by direct user feedback across multiple rounds.
5. Restyle the curves three times in sequence per explicit user requests: strip fill → fill with background color → fill with the series' established gray/black "line 1 == line 6" / "line 1 != line 6" convention — saving the middle "no-fill" state as a named template first (`FX-nums-noFill`).
6. Commit the session's work (in progress — this document was requested mid-commit-sequence).
</original_task>

<work_completed>

## 1. Verified actual disk state of the body-schema files (contradicted the prior handoff's assumptions)

The paused handoff (`whats-next.md` at session start) said numbering was "unresolved" and asked which of 5 candidate files was canonical. Direct inspection found:

- `diagrams/FX-body-schema-layers-01.svg` (146KB → grew to 157KB during this session) was already far more complete than the handoff assumed: **all 64 hexagram numbers were already placed**, not just 2.
- Verified computationally (not by eye): right-hand column reads exactly 1–64 in ascending y-order, no gaps/duplicates; left-hand column correctly cross-references each quartet's ribbon partner (matches the `FX_to_KW.md`/`Spinal_Mapping.md`-derived ribbon table from the prior session, e.g. row 5↔33, row 27↔40).
- Rendered via headless Chromium screenshot (`chromium-browser --headless --disable-gpu --no-sandbox --screenshot=... --window-size=900,1300 file://...`, written to `$HOME` — nested scratchpad paths still fail with "Permission denied", confirmed again this session) — legible, no illegible-overlap problem.
- One inconsistency found and explicitly accepted by the user as intentional (not a bug): the 4 "axis-only" pairs (`FX{1,2}`, `FX{25,26}`, `FX{37,38}`, `FX{61,62}`) show the *same* number on both left/right labels (e.g. row 1 shows "1/1"), while the other 4 pairs (`FX{15,16}`, `FX{23,24}`, `FX{43,44}`, `FX{51,52}`) correctly cross-reference their partner (row 15 shows "15/16"). User's answer via AskUserQuestion: "Leave as-is."
- Confirmed the "Numbers" Inkscape layer promotion (`inkscape:groupmode="layer"`) never happened — the imported digits sit as flat, ungrouped elements at the SVG root, interleaved in document order as `(fill-path, stroke-path, text)` triplets per number. Not a blocker, just noted.

## 2. Diagnosed and answered a live Inkscape question about Align & Distribute

User reported the "Relative to: Selection" option had disappeared from Align & Distribute, leaving only Page/Drawing. Diagnosed: this happens whenever only **one** object is selected (Inkscape needs ≥2 selected objects to offer selection-relative alignment). Gave the fix: select both the number's circle and its text (click one, `Shift`+click the other), then `Relative to: Last selected` (selecting the reference object last), with "Treat selection as group" unchecked. Also flagged a related font-metrics caveat (single-digit glyphs are narrower than two-digit ones, so per-glyph centering may need revisiting number-by-number) — not something the user hit in practice this session, no further action needed.

## 3. Found and fixed an incomplete grouping structure in `FX-body-schema-layers-01.svg`

User had begun "grouping all the numbers in their circles." Audit found the grouping was structurally incomplete:
- All 128 `FX_rightNumCirc_NN`/`FX_leftNumCirc_NN` groups existed and were correctly named (matching the digit each displays), but **each contained only the stroke-ring path** — the white fill-disc and the digit `<text>` were still loose, ungrouped siblings at the SVG root (except group `FX_rightNumCirc_01`, which uniquely already had its text, an artifact of the user's first manual test).
- Verified via classification script: 128 loose fill-disc paths (all of them), 128 stroke-rings correctly grouped, only 1 text (`text44`) correctly grouped.
- **Fixed programmatically in two passes** (both backed up first, backups in `/tmp/claude-.../scratchpad/FX-body-schema-layers-01.svg.bak` and `.bak2` — ephemeral, not in repo):
  1. Verified (before touching anything) that every NumCirc group's immediately-preceding top-level sibling was its matching fill-disc (128/128 matched, 0 problems) — then moved each fill-disc to be the first child of its group.
  2. Verified every group-without-text was immediately followed by its matching `<text>` (127/127 matched, digit content cross-checked) — then moved each text to be the last child of its group.
- Final verified state: all 128 groups contain exactly `[fill-disc, stroke-ring, text-digit]` in correct paint order. No duplicate IDs (checked via `Counter` over every `id` in the document). Render confirmed **pixel-identical** (MD5 hash match) before/after both fixes — purely structural, zero visual change.

## 4. Re-embedded the finished geometry into `diagrams/spine02/Spine_Page1_FX.html`

- Extracted exactly 148 elements from `FX-body-schema-layers-01.svg` (the 20 `FX{...}`-labeled ring/pair elements + all 128 `NumCirc` groups) via lxml, in original document order, stripping the auto-added `xmlns` cruft lxml injects per-fragment (the file's existing convention — confirmed from the pre-existing embed — is to keep bare `inkscape:label` attributes with no `xmlns:inkscape` declaration; browsers tolerate this fine in HTML5 foreign-content parsing).
- Replaced the old numbers-free `<svg class="spine-svg" viewBox="0 0 595 842" ...>...</svg>` block in `Spine_Page1_FX.html` with the new 148-element content, keeping the same outer `<svg>` attributes (only the `aria-label` was updated to mention hexagram numbers).
- **Discovered and worked around a real browser-compatibility issue**: dvisvgm's number-digit `<text class="f0">` elements depend on deprecated SVG-font (`<font>`/`<glyph>`/`<font-face>`) elements in `<defs>`, which **no modern browser renders** (Chrome/Firefox dropped SVG-font support years ago). The digits were only rendering because browsers silently fall back to a generic system font per-CSS-property when the named `font-family` fails to resolve, while other properties in the same CSS rule (font-size) still apply. Decision: **did not embed the ~36KB of glyph-outline `<defs>` data at all** (skipped `defs13`, kept none of the SVG-font machinery) — instead added one scoped CSS rule, `.spine-svg text.f0 { font-family: var(--font-mono); font-size: 5.68px; }`, giving the digits an intentional, theme-consistent fallback font instead of an accidental one. Deliberately did **not** set `text-anchor`/`dominant-baseline` on this rule, since the digit `x`/`y` positions were manually hand-centered by the user assuming default (start-anchored) positioning — changing anchor would have silently undone that work.
- Verified: exact element counts (20 `FX{...}` labels, 64 right + 64 left NumCirc groups) via regex count on the written HTML; `xmllint --html --noout` clean.

## 5. Fixed a real display-scale legibility problem (multi-round, user-driven)

- First screenshot at an arbitrarily narrow 1000×1400 test window showed the numbers as unreadable ~2.6px noise, because the page's `.single-panel-wrap` CSS (a deliberate design constraint reproducing "the width one grid column would get," per its own code comment) caps a single-panel page far narrower than the diagram's hand-tuned digit font-size (5.68 SVG user-units) was ever going to survive at typical scale.
- Re-tested at a wider, more realistic window (1800px) to avoid a false alarm from an unrealistically narrow test — still small, confirmed a real problem, not a test artifact.
- **User's explicit decision** (via AskUserQuestion, two options offered): "Enlarge the whole diagram" (preserve hand-tuned circle/digit proportions, widen the display container) over "scale up just the number groups" (would change proportions relative to the ring linework). Implemented via a new page-scoped CSS class `single-panel-wrap--diagram { width: min(1200px, 94vw); }` applied only to this page's wrap div (does not affect other `spine02/` pages, each of which has its own inline `<style>` block).
- **User reported still "much too small" at their actual screen (1920×1080, Zen browser)**, suggesting "300% larger." Investigated *why* rather than just cranking the width blindly:
  - Discovered the source SVG's `viewBox="0 0 595 842"` wastes real margin — computed the **exact** bounding box of all 148 kept elements via `inkscape --query-all` (cross-referenced against the known Inkscape px↔pt unit-conversion factor, 96/72 = 1.3333, verified against known reference points like n=1's cy=80.708 and the FX{3,4,63,64} ring's known y-range 100.754–712.176 — both matched within rounding). Result: real content bbox is `x:[120.542, 447.299]` (width 326.758), `y:[75.707, 715.914]` (height 640.206) — i.e. only ~55% of the nominal 595×842 canvas is actually used.
  - Tightened the embedded `<svg>`'s `viewBox` to `110 65 348 661` (bbox + ~10-unit padding) — a "free" ~1.7x scale gain with zero clipping risk (verified against the computed geometry, not eyeballed).
  - Combined with widening the container further: `single-panel-wrap--diagram { width: min(1900px, 96vw); }`.
  - Combined effect at 1920px screen: ~2.6x size increase over the previous (already-once-enlarged) state — short of the literal 3x requested, because true 3x would require the container to exceed ~96vw and force horizontal scrolling. **Explicitly told the user this tradeoff and why**, rather than silently under-delivering or silently allowing overflow; user did not object or ask for more.
  - Verified at exactly 1920×1080 (user's actual screen size): no horizontal scrollbar, dense middle band (rows 27–45) stays legible, footer (name-tag/title/nav) renders undamaged below the now much-taller diagram (confirmed via a 1920×6000 tall-viewport render + background-color row-scan to find the true content extent, 4286px, well short of any clipping).

## 6. Three sequential curve-fill restyling passes (all on `diagrams/spine02/Spine_Page1_FX.html`)

All three passes operated on a precisely bounded "ring block" substring of the file — from the `<svg class="spine-svg"...>` opening tag to (but excluding) the first `id="FX_rightNumCirc_01"` — established each time via `grep -n` to get exact current line numbers before scripting the edit (line numbers shift between passes as content grows). Every pass verified: (a) the 128 number-circle groups' `#ffffff` fill count stayed exactly 128 and no new color leaked into that block, (b) `xmllint --html --noout` clean, (c) a Chromium screenshot.

- **Pass A — strip fill from curves, keep number-circle fill** (user's literal request: "take the fill out of all the curves but keep the fill only in the numberCircles"): replaced `fill:#ffffff` → `fill:none` and `fill="#fff"` → `fill="none"` within the ring-block scope only. 52 style-level substitutions. Verified visually: rings became clean stroke-only outlines, numbers stayed filled/legible.
- **Pass B — fill curves with the page background color** (user's literal request): replaced `fill:none`/`fill="none"` (the ring-block values from Pass A) with `fill:var(--paper)`/`fill="var(--paper)"` — deliberately used the page's existing CSS custom property rather than a hardcoded hex, so it automatically follows the page's existing light/dark theme system (same variable the body background and `.name-tag` already use). 50 style-level + 36 attribute-level substitutions. Verified light-mode screenshot matches background exactly (curves visually disappear except for their black stroke outline, correctly re-occluding whatever crosses behind them — same visual effect as the original solid-white rendering, but theme-correct). A forced-dark-mode Chromium screenshot was attempted for a dark-mode check but is **not fully trustworthy** — Chromium's `--force-dark-mode`/`--enable-features=WebContentsForceDark` flags do heuristic auto-repainting, not `prefers-color-scheme` emulation, and this environment has no Playwright/DevTools-protocol tool available to do a proper media-feature emulation (Playwright MCP is confirmed broken here, per longstanding note). **If real dark-mode correctness of this page ever needs verifying, it must be checked in an actual browser, not via this environment's headless tooling.**
- **Pass C — gray/black fill per the series' established "line 1 == line 6" convention** (user clarified this is what the whole 10-page series is actually about; pages 4/9 = `Line1eq6`, pages 5/10 = `Line1ne6`). **Re-derived the ground-truth color assignment directly from the original, untouched `diagrams/spine/Spine_Page1_FX.html`** (not from memory/assumption) — confirmed the existing CSS rule pattern in `diagrams/spine/Spine_Page4_Line1eq6.html`: `.ribbon-3132 { fill: var(--ink-faint); fill-opacity: 0.8; stroke: var(--ink-faint); }` (gray) vs `.ribbon-3334 { fill: var(--ink); fill-opacity: 0.8; stroke: var(--ink); }` (black), with `.pair-ellipse-*`/`.group-circle-*` (the 8 small adjacent-pair markers in the *old* ribbon-based design) staying unfilled-outline-only even on the "filled" pages. Extracted the exact class assignment from the original `Spine_Page1_FX.html`'s actual ribbon/pair-ellipse/group-circle elements (by parsing `class="..."` + `cx`/`cy` against the known `y = 40 × row` pitch), independently re-deriving and cross-checking against the prior session's already-verified ribbon table. Final 20-group assignment (10 gray / 10 black, exhaustive, sums to exactly 20):
  - **Gray** (`var(--ink-faint)`): `FX{1,2}`, `FX{25,26}`, `FX{37,38}`, `FX{61,62}`, `FX{5,6,33,34}`, `FX{9,10,17,18}`, `FX{13,14,49,50}`, `FX{21,22,41,42}`, `FX{29,30,57,58}`, `FX{45,46,53,54}`
  - **Black** (`var(--ink)`): `FX{15,16}`, `FX{23,24}`, `FX{43,44}`, `FX{51,52}`, `FX{3,4,63,64}`, `FX{7,8,31,32}`, `FX{11,12,47,48}`, `FX{19,20,55,56}`, `FX{27,28,39,40}`, `FX{35,36,59,60}`
  - **Design decision (not a literal copy of the old page):** applied the fill+opacity treatment to **all 20** groups (both the 12 quartets *and* the 8 adjacent pairs), even though the original page only filled the 12 ribbon/quartet curves and left the 8 pair-markers as unfilled outlines. Reasoning: in the *old* page, pairs were tiny decorative markers, not real curves; in the *new* body-schema-based page, all 20 groups (pairs included) are real visible ring/arc geometry, so applying the coloring rule uniformly is the more faithful transfer of intent. This was a judgment call, not confirmed explicitly by the user in these words — flag if they push back.
  - Implemented via lxml: for each of the 20 top-level labeled elements, walked itself + all descendant `<path>`s, parsed each `style` attribute into a dict, set `fill`/`stroke` to the resolved color var, set `fill-opacity: 0.8`, rebuilt the style string, and also tidied the (redundant, style-overridden) bare `fill=`/`stroke=` presentation attributes to match. Verified: 20/20 labels processed, assertion that every label falls in exactly one of GRAY/BLACK (no missing, no double-assignment).
  - Screenshotted at 1920×1080 (top of diagram) and the dense middle band (rows 27–45): confirmed correct alternating gray/black per the table (e.g. outermost ring `FX{3,4,63,64}` black, next-in `FX{5,6,33,34}` gray, next `FX{7,8,31,32}` black, ...), numbers still crisply legible on top throughout.

## 7. Saved the no-fill state as a named template (user request, executed slightly out of order)

- **Ordering mistake, caught and corrected in-session**: user asked to (a) save the current no-fill page as a template named `FX-nums-noFill`, *then* (b) apply the gray/black fill. Pass C (gray/black) was implemented first, before the template save — the no-fill HTML state was never separately written to disk before being overwritten in place.
- **Recovered without data loss**: since the no-fill→background-color→gray/black transformations were all known, scripted, invertible edits (not manual/lossy), reconstructed the no-fill state by copying the *current* (gray/black) `Spine_Page1_FX.html` to `diagrams/spine02/Spine_Page1_FX-nums-noFill.html`, then running the inverse transform on its ring block only (`fill` → `none`, drop `fill-opacity`, `stroke` → hardcoded `#000000`/`#000`, matching exactly what Pass A had produced).
- **Verified byte-exact correctness**: screenshotted the reconstructed template and MD5-compared against the actual screenshot taken live during Pass A earlier in the session — **hashes matched exactly** (`d5c2b52dbb1ffb4af7aa27b34dd27258`), proving zero information was lost despite the ordering slip.
- Current repo state: `diagrams/spine02/Spine_Page1_FX-nums-noFill.html` holds the no-fill template (viewBox `110 65 348 661`, container width `min(1900px, 96vw)`, numbers grouped and legible, curves stroke-only black, no fill). `diagrams/spine02/Spine_Page1_FX.html` (the live/canonical page) holds the gray/black-filled version.

## 8. Notes hygiene fix (prep for commit, this document's triggering context)

- `notes/tools/dvisvgm-output-inkscape-edit.md`'s `## Status` section was stale (said FX-body-schema prep was "planned but not yet done" as of 2026-08-16) — the prior session's own handoff had already flagged this as needing a fix "whenever it's next touched." Updated it (this session, 2026-08-17) to accurately describe: the FX prep is done, `KW-body-schema.svg` is still raw/untouched, and the spine02 page-1 renovation status (numbered, gray/black-filled, pages 2–10 still old-style).

</work_completed>

<work_remaining>

## Immediate — finish the in-progress commit

The user said "yes, let's commit" and I was mid-way through staging when this handoff was triggered. Plan (not yet executed, or only partially executed — **check `git status` / `git log` first to see how far it got**):

1. **Commit 1 — carryover docs from the prior session** (untouched this session except the Status-line fix just made):
   - `notes/tools/dvisvgm-howto.md` (modified: added a cross-reference link to `dvisvgm-output-inkscape-edit.md`)
   - `notes/tools/inkscape-howto.md` (modified: same, added cross-reference link)
   - `notes/tools/dvisvgm-output-inkscape-edit.md` (new file from prior session + Status section just corrected this session)
2. **Commit 2 — this session's diagram/spine work**:
   - `diagrams/FX-body-schema.svg` (stable master ring-only reference, untouched this session, never committed)
   - `diagrams/FX-body-schema-layers-01.svg` (the canonical numbered/grouped working file, extensively modified this session — grouping fixes)
   - `diagrams/KW-body-schema.svg` (untouched raw dvisvgm output, companion to FX, never committed — legitimate source asset even though unprocessed)
   - `diagrams/spine02/` (the whole sandbox directory — only `Spine_Page1_FX.html` and the new `Spine_Page1_FX-nums-noFill.html` differ from plain copies of `diagrams/spine/`; the other 9 pages are untouched faithful copies, included for completeness of the sandbox)
   - `whats-next.md` (this refresh)
3. **Deliberately left uncommitted / excluded from staging** (still on disk, untracked, harmless): `diagrams/FX-body-schema-layers.svg`, `diagrams/FX-body-schema-layers-02.svg`, `diagrams/FX-body-schema-wNums.svg`, `diagrams/FX-body-schema-wNums.svg.2026_08_16_21_18_17.0.svg` — all superseded intermediate/abandoned states from the numbering exploration (Interpolate-extension attempts, early layer-import tests), now fully obsoleted by `FX-body-schema-layers-01.svg`. **Did not delete them** (only asked to commit, not to clean up) — flag to the user that these exist and ask if they want them deleted, since committing them would clutter history with dead ends.
4. After committing, **remind the user about `git push`** per their standing preference (see `[[feedback_push-reminder]]` in Claude's memory system) — nothing has been pushed to `origin/master` yet this session.

## After the commit

1. **Pages 2–10 of `spine02/`** are still untouched copies of the original ribbon-based style — explicitly out of scope until page 1 is fully approved (a scoping decision from an even earlier session, never revisited, still holds).
2. **Dark-mode visual correctness of `Spine_Page1_FX.html`/`Spine_Page1_FX-nums-noFill.html` has not been reliably verified** — this environment's headless-Chromium tooling can't properly emulate `prefers-color-scheme`. If dark mode matters before calling page 1 fully done, it needs a real-browser check (the user's own Zen browser, toggling `data-theme` or OS dark mode) rather than another attempt at headless verification here.
3. **The gray/black fill applied to all 8 pair groups (not just the 12 quartets) was a judgment call**, diverging from the old page's behavior (which left pair-markers unfilled). Not yet explicitly confirmed by the user — watch for pushback and be ready to revert just the 8 pairs to unfilled-outline if they'd rather match the old page exactly.
4. **`KW-body-schema.svg` has not had the FX-style grouping/labeling/numbering treatment applied** — if a `spine02` page for the KW (King Wen) sequence is ever wanted using this same nested-ellipse-with-numbers style, that whole grouping+numbering+embedding pipeline (Sections 1–4 of this document, effectively) would need to be redone from scratch for the KW file. Not requested yet.
5. The four superseded body-schema SVG variants (see item 3 above) remain on disk untracked — resolve (delete or keep) per user preference next time it comes up.

</work_remaining>

<attempted_approaches>

- **Committing before saving the `FX-nums-noFill` template** — the user asked for save-template-then-recolor, but Pass C (gray/black) was actually run first by mistake. Recovered via reconstruction rather than repeating the user's request-flow; verified byte-exact via screenshot MD5 comparison. Not a dead end exactly, but worth noting the ordering slip in case the user asks why the template file's git history (once committed) doesn't show it being created before the color change.
- **Literal 3x diagram enlargement** — user explicitly suggested "300% larger." Determined this is physically impossible without horizontal overflow on a 1920px-wide screen (would need a ~2075px-wide container against ~1872px of actual available space). Delivered the maximum safe alternative (~2.6x, via viewBox-crop + width cap at 96vw) and explained the physical ceiling rather than either silently under-delivering or silently allowing horizontal scroll. User did not push back on landing short of 3x — but this is a live option (allow overflow/horizontal scroll) if they ever do.
- **Forced-dark-mode headless screenshot for verifying `var(--paper)`/dark-theme correctness** — attempted via `chromium-browser --force-dark-mode --enable-features=WebContentsForceDark`. Produced a render, but this flag does Chromium's own heuristic auto-repaint, not standards-based `prefers-color-scheme` emulation, so it's not trustworthy evidence either way. No working alternative found in this environment (Playwright MCP confirmed broken again, per longstanding note carried over from before this session). Flagged as an open verification gap rather than papered over.
</attempted_approaches>

<critical_context>

## Full 20-group gray/black color table (load-bearing, re-derive-verified, do not re-guess)

**Gray** (`var(--ink-faint)`, fill-opacity 0.8): `FX{1,2}`, `FX{25,26}`, `FX{37,38}`, `FX{61,62}`, `FX{5,6,33,34}`, `FX{9,10,17,18}`, `FX{13,14,49,50}`, `FX{21,22,41,42}`, `FX{29,30,57,58}`, `FX{45,46,53,54}`

**Black** (`var(--ink)`, fill-opacity 0.8): `FX{15,16}`, `FX{23,24}`, `FX{43,44}`, `FX{51,52}`, `FX{3,4,63,64}`, `FX{7,8,31,32}`, `FX{11,12,47,48}`, `FX{19,20,55,56}`, `FX{27,28,39,40}`, `FX{35,36,59,60}`

Source of truth: `diagrams/spine/Spine_Page4_Line1eq6.html`'s `.ribbon-3132`/`.ribbon-3334` CSS rules, cross-referenced against `diagrams/spine/Spine_Page1_FX.html`'s actual `class="ribbon ribbon-31{32,34}"` / `class="pair-ellipse-31{32,34}"` / `class="group-circle-3132"` elements (parsed by `cx`/`cy` against the `y = 40 × row` pitch established in the prior session). This whole series (`Spine_Page1`–`10`) is fundamentally about the "line 1 == line 6" (gray) vs "line 1 != line 6" (black) property of each hexagram pair/quartet — confirmed directly by the user this session, correcting an earlier session's incomplete understanding of what the `-3132`/`-3334` class-name suffixes meant.

## The full n → (cx, cy) position table (from the prior session, still the ground truth if any position ever needs recomputing)

`cx = 288.932` for every hexagram number **except** n ∈ {1, 2, 25, 26, 37, 38, 61, 62} (the 4 axis-only pairs), which use `cx = 283.920`. `cy` runs from 80.708 (n=1) to 712.176 (n=64) in a clean arithmetic progression, spacing ≈10.023/10.024 units (dvisvgm's universal "notch" constant, 168 occurrences confirmed in the source file). Full per-n table is in the prior session's `whats-next.md` if ever needed again verbatim — not reproduced here since this session never needed to recompute individual positions (only the aggregate bounding box, which *was* recomputed fresh this session — see below).

## Exact bounding box of the kept diagram content (load-bearing for the viewBox crop)

Computed via `inkscape --query-all FX-body-schema-layers-01.svg`, filtered to the 148 kept element IDs, converted from Inkscape's query units (px at 96dpi) to the file's native user-units (pt at 72dpi) by dividing by 96/72 = 1.3333 (verified against known reference points, e.g. n=1's `cy=80.708` and the `FX{3,4,63,64}` ring's known y-range 100.754–712.176, both matched within rounding after conversion):

`x: [120.542, 447.299]` (width 326.758), `y: [75.707, 715.914]` (height 640.206)

The embedded `<svg>`'s current `viewBox` is `110 65 348 661` (bbox + ~10-unit padding all sides). If the number-circle groups or ring geometry are ever edited further (e.g. re-centering), this bbox — and therefore the viewBox — may need recomputing; don't assume `110 65 348 661` stays correct forever, it's only correct for the exact geometry as of this session's end.

## Page-scoped CSS additions to `Spine_Page1_FX.html` (and mirrored in the `-noFill` template except for color)

```css
.single-panel-wrap--diagram { width: min(1900px, 96vw); }
.spine-svg text.f0 { font-family: var(--font-mono); font-size: 5.68px; }
```
The wrap div carries `class="single-panel-wrap single-panel-wrap--diagram"`. This override is scoped to this one file's own inline `<style>` block — it does **not** affect any other `spine02/` page, since each page has its own independent inline stylesheet (confirmed, this is not a shared external CSS file).

## Environment / tooling notes (carried over + reconfirmed this session)

- Inkscape 1.4.3, apt package (not snap/flatpak) — confirmed again this session via successful `inkscape --query-all` CLI usage (new tool usage this session, worked cleanly, no sandboxing issues).
- Headless-Chromium screenshot command, reconfirmed multiple times this session:
  ```
  chromium-browser --headless --disable-gpu --no-sandbox --screenshot=<path> --window-size=<W>,<H> file://<absolute-path>
  ```
  Must write to `$HOME` or similar — nested Claude scratchpad paths still fail with "Permission denied" (reconfirmed, same as prior session).
- **Playwright MCP still does not work in this environment** — reconfirmed by necessity this session (needed proper `prefers-color-scheme` emulation for dark-mode verification and had no working alternative). If this environment ever gets a working browser-automation MCP tool, dark-mode verification of the spine pages should be redone properly.
- Chromium's `--force-dark-mode`/`--enable-features=WebContentsForceDark` flags exist and produce *a* dark render, but it's heuristic auto-repainting, not real `prefers-color-scheme` emulation — don't trust it as evidence of correct CSS `var(--paper)`/`data-theme` behavior.
- `inkscape --query-all <file>` reliably bulk-dumps `id,x,y,width,height` (visual bounding box, includes stroke) for every element with an `id` in one shot — much faster than querying one `--query-id` at a time. Units are Inkscape's internal px-at-96dpi; divide by 1.3333 to get the file's native user-units when (as here) the SVG declares `width="...pt"`.
- lxml (`from lxml import etree`) was used throughout this session for precise, verifiable SVG surgery (parsing `style` attributes into dicts rather than fragile string-replace, moving elements while preserving attribute/child order, etc.) — preferred consistently over regex-only approaches once anything beyond a flat find/replace was needed. The one recurring gotcha: `etree.tostring()` on an extracted fragment auto-injects `xmlns`/`xmlns:inkscape` declarations that the target HTML file's existing convention doesn't use — always strip via `re.sub(r'\s+xmlns(:\w+)?="[^"]*"', '', s)` before splicing into the HTML.

## User's demonstrated preferences (this session)

- Prefers exact computed/verified answers over eyeballing, consistent with the standing memory `[[feedback_verification-standard]]` — every restyling pass this session was scoped-and-counted before/after, not just screenshotted.
- When given a two-option tradeoff (e.g. "enlarge whole diagram" vs "scale up number groups"; later, implicitly, "2.6x with no overflow" vs "true 3x with overflow"), engages with the *reasoning*, not just the outcome — worth continuing to explain physical/technical ceilings explicitly rather than silently landing short of a literal request.
- Corrects course readily and without friction when told about a mistake (the template-ordering slip) — no need to over-apologize, just fix it and show the verification that nothing was lost.

</critical_context>

<current_state>

## Files — diagrams/

- **`FX-body-schema.svg`** — stable, finalized, unchanged this session. Still the master ring-only reference. Untracked, not yet committed (planned for Commit 2).
- **`FX-body-schema-layers-01.svg`** — the canonical numbered/grouped working file. All 64 numbers placed, all 128 fill+stroke+text groups correctly assembled this session. This is now the authoritative source the `spine02` embed was pulled from. Untracked, not yet committed (planned for Commit 2).
- **`FX-body-schema-layers.svg`, `FX-body-schema-layers-02.svg`, `FX-body-schema-wNums.svg`, `FX-body-schema-wNums.svg.2026_08_16_21_18_17.0.svg`** — superseded intermediate states from the numbering exploration, fully obsoleted. Untouched this session. **Deliberately excluded from the commit plan** — still on disk, untracked. Ask the user whether to delete.
- **`KW-body-schema.svg`** — raw, unprocessed dvisvgm output, companion to FX. Untouched this session. Untracked, not yet committed (planned for Commit 2, as a legitimate source asset even though unprocessed).
- **`spine02/`** — sandbox copy of `spine/`. `Spine_Page1_FX.html` now holds the fully finished page-1 renovation: embedded ring+number geometry (148 elements), tightened viewBox (`110 65 348 661`), widened container (`min(1900px, 96vw)`), gray/black curve fill per the verified 20-group table. `Spine_Page1_FX-nums-noFill.html` is the newly-added, verified-byte-exact no-fill template variant. The other 9 pages are untouched faithful copies of `spine/`. Untracked, not yet committed (planned for Commit 2).

## Files — notes/

- **`notes/tools/dvisvgm-howto.md`**, **`notes/tools/inkscape-howto.md`** — modified (cross-reference links added) in the *prior* session, untouched this session except being carried forward uncommitted. Planned for Commit 1.
- **`notes/tools/dvisvgm-output-inkscape-edit.md`** — new file from the prior session; its `## Status` section was corrected *this* session (see Work Completed §8) to stop saying the FX prep is "not yet done." Planned for Commit 1.

## Git

- `git status` as of this document's writing (re-verify, may have changed if commits were already made before this handoff was triggered):
  - Modified, unstaged: `notes/tools/dvisvgm-howto.md`, `notes/tools/inkscape-howto.md`, `whats-next.md` (this file)
  - Untracked: `diagrams/FX-body-schema-layers-01.svg`, `diagrams/FX-body-schema-layers-02.svg`, `diagrams/FX-body-schema-layers.svg`, `diagrams/FX-body-schema-wNums.svg`, `diagrams/FX-body-schema-wNums.svg.2026_08_16_21_18_17.0.svg`, `diagrams/FX-body-schema.svg`, `diagrams/KW-body-schema.svg`, `diagrams/spine02/`, `notes/tools/dvisvgm-output-inkscape-edit.md`
- **Nothing committed or pushed yet this session.** The user said "yes, let's commit" immediately before this handoff-writing was triggered — the two-commit plan above (docs, then diagram work) was decided but execution had not yet started (or was only just starting) when this document was requested. **Check `git log` first to see if either commit actually landed before continuing.**
- Branch is `master`, up to date with `origin/master` (no local commits ahead as of session start).

## Open questions for whoever continues this

1. Did the planned two-commit sequence (docs, then diagrams/spine work) actually execute before this handoff was written? Check `git log --oneline -5` first.
2. Should the 4 superseded body-schema SVG variants be deleted, or left as untracked scratch files indefinitely? Not yet asked.
3. Does the user want dark-mode correctness verified in a real browser before considering page 1 fully done? Not yet asked — flagged as a known verification gap.
4. Is applying the gray/black fill to all 8 pair-groups (not just the 12 quartets, diverging from the old page's pair-ellipse/group-circle-stays-unfilled behavior) actually correct per the user's intent, or should pairs revert to unfilled outlines? Judgment call, not explicitly confirmed.
5. After the commit, remind the user about `git push` to `origin/master` (GitHub Pages auto-deploys from master) — per their standing preference, not yet done this session.

</current_state>
