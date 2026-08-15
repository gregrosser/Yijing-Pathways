<original_task>
"@Yijing-Pathways/ review" — an open-ended review of the Yijing Pathways project. Interpreted (and confirmed by the flow of the session) as a full project health review: repo hygiene, link integrity, the interactive diagram pages, the research notes, and the correctness of the underlying hexagram data. The user then directed fixes in stages: first "yes" to the mechanical batch (review items 1, 2, 6, 8), then "take care of items 3 and 4 now", then "push to master", then "refresh the whats-next" (this document).
</original_task>

<work_completed>

## Phase 1 — the review itself (no files changed)

**Data-layer verification (programmatic, not by reading).** Extracted the embedded JS tables from the diagram pages with Python and checked them:
- `HEXLINES` — 64 entries, all distinct; the odd/even complement rule (hexagram n odd is the exact bit-inverse of n+1) holds for all 32 pairs.
- `GROUPS` (20 groups) — members partition 1..64 exactly; every `dual` link is reciprocal; every group's `axis` field agrees with the line-1-vs-line-6 rule computed independently from `HEXLINES`.
- `distance` field — initially appeared wrong; my first check assumed `|a-b|`. The actual rule is **`distance == |a-b|/2 + 1`** (counts pair-positions inclusive, since hexagrams sit in adjacent pairs). Under the correct formula all 12 quartets are self-consistent with zero exceptions. **The data was right; my check was wrong.**
- `FX_TO_KW` — a true bijection; the hardcoded table in `group-table.html` matches the `data-kw` DOM attributes in both `kw-square.html` and `FX_circle_KW_square.html`, and matches all 64 rows of the HTML table in `notes/structure/FX_to_KW.md`.
- `HEXLINES` and `GROUPS` are **byte-identical (md5-compared)** across `FuXi21.html`, `FX_circle_KW_square.html`, `kw-square.html`.

**Link integrity.** Resolved every non-external `href`/`src` across all 16 HTML pages — all targets existed, no `file://` leftovers, all note wikilinks resolved. (This check had a blind spot — see Phase 3.)

**Findings, as reported and ranked:**
1. No `<!DOCTYPE html>` on any of the 16 pages (no `<html>`, `<head>`, `<body>`, `lang`, or `charset` either) → whole site rendered in quirks mode.
2. No `<meta viewport>` anywhere → desktop-width rendering on phones.
3. Spine pages / `kw-square.html` reachability (**partly wrong as first stated — corrected in Phase 3**).
4. `notes/` published in the public repo but unreachable from the site; `Spinal Mapping` index entry was an unlinked "Note" placeholder.
5. ~19 MB of duplicated PDFs: `collectionPDFs/*.pdf` vs `collectionPDFs/view/*.pdf` — same 13 documents, identical page counts, sizes within ~0.1% (the `view/` copies are Ghostscript re-runs). Only `view/` is linked from anywhere. Repo is 75 MB working tree + 35 MB `.git`.
6. Stale `local` meta labels on 4 index entries, left from before publication.
7. Hexagram data hand-synced across 4 files (3 byte-identical copies + 1 hardcoded `FX_TO_KW`).
8. Stray untracked `TO-DOS.md.tmp.21047.e880bdb92401`, byte-identical to `TO-DOS.md`; `.gitignore` was a single line so `git add -A` would have published it.
9. `design.md` loose end: the empty Figma file "PDF Collection Design Reference" still undecided (populate as index, or remove).

## Phase 2 — mechanical batch (items 1, 2, 6, 8)

- Prepended to all 16 pages (`index.html`, `diagrams/*.html`, `diagrams/spine/*.html`; `archive/` deliberately left alone):
  `<!DOCTYPE html>` / `<html lang="en">` / `<meta charset="utf-8">` / `<meta name="viewport" content="width=device-width, initial-scale=1">`
- Removed all four stale `local` labels from `index.html`.
- Deleted the stray `.tmp` file; expanded `.gitignore` with `*.tmp`, `*.tmp.*`, `*~`, `.DS_Store` (tested with a dummy file — correctly ignored).

**Verification:** before/after headless-Chromium screenshots of 6 pages, pixel-diffed with ImageMagick `compare -metric AE`. First pass showed `index.html` differing by 26% — but two runs of the *same unmodified file* also differed by 26%, proving nondeterminism (the IntersectionObserver fade-in), not regression. Re-ran with `--force-prefers-reduced-motion` (the CSS has a `prefers-reduced-motion` block pinning opacity to 1): same file twice = 0 pixels, and orig-vs-new = **0 differing pixels on all six pages**. Confirmed `document.compatMode === "CSS1Compat"`.

**Mobile overflow measured** by injecting a probe script and reading `documentElement.scrollWidth` vs `clientWidth` at narrow width:
- `index.html`, `kw-square.html`, `FuXi21.html` — no overflow, genuinely responsive (the CSS already used `min(85vw, …)` and media queries; it just never had the viewport tag to activate them)
- `group-table.html` — 711 vs 485 (+226px), horizontally scrollable
- `FX_circle_KW_square.html` — 723 vs 485 (+238px), horizontally scrollable
Content is reachable by panning, not lost.

## Phase 3 — items 3 and 4

**Correction to review item 3.** The spine pages were **not** unreachable. All 11 had a `next-link`, and pages 1→2→…→10→1 formed a complete forward ring, so all ten were reachable from the index. What was actually broken was narrower:
- forward-only navigation (no prev-links)
- no back-link to the index on any spine page (unlike the other diagram pages, which have a `← Yijing Pathways` footer)
- `Spine_Prototype_Both.html` was a true orphan (nothing linked to it) with a dead `next="#"`

**Spine nav rebuild** (Python script rewriting both the CSS rule block and the markup block in all 10 pages):
- added `.prev-link` (mirrored chevron SVG, `M40 20 L24 32 L40 44`), sharing hover/transition rules with `.next-link`
- added `.nav-center` block with `PAGE n / 10` counter (`.nav-count`) and `.nav-home` → `../../index.html`
- `.nav-row` changed from `justify-content: center` to centered flex with `gap: 32px`
- kept the 10→1 wrap, so the ring is now closed in both directions (page 1's prev is page 10)
- verified the full prev/next/home graph programmatically and by screenshot

**Other item-3 work:**
- `git mv diagrams/spine/Spine_Prototype_Both.html archive/old-architecture/` (user chose "move to archive")
- added a "King Wen Square" entry to the Structure strand linking the orphaned `diagrams/kw-square.html`

**Item 4 — notes published via Jekyll** (user chose "Jekyll front matter + layout"):
- Created `_layouts/note.html` matching the index design system: same palette vars, same font stack (`'Iowan Old Style', 'Palatino Linotype', Palatino, 'URW Palladio L', P052, Georgia, serif` — the Palladio identity `design.md` documents as the collection's strongest brand signal), `.eyebrow` strand label, styled tables/code/blockquote, `← Yijing Pathways` footer at `../../index.html`, and `.note-body { overflow-x: auto }` so the wide hand-written tables stay reachable.
- **Layout deliberately does not emit its own `<h1>`.** Each note already begins with `# Title`; the layout styles `.note-body > h1:first-child` to carry the header rule instead. This avoided duplicate headings *and* avoided editing note bodies.
- Added front matter (`layout: note`, `title:`, `strand:`) to all 6 notes.
- Converted all 6 Obsidian wikilinks to relative markdown links. **Targeted `.md`, not `.html`** — see attempted_approaches.
- Fixed two genuinely broken links in `Spinal_Mapping.md` (`FX_spine_axis_31_32.html` / `_33_34.html`) which actually live in `archive/old-architecture/` — now `../../archive/old-architecture/…`.
- Index wiring: converted the three "Note" placeholder `<div>`s into `<a class="entry">` links (Spinal Mapping, Chinese Culture, FuXi Sequence Origins) and added two new note entries ("Group Table — Observations", "FX → KW — Correspondence & Verification"). Checked for nested anchors (invalid HTML) — none; the existing diagram cards are already `<a class="entry">` wrappers, which is exactly why the notes became separate entries rather than nested secondary links.

**Verification of the Jekyll work without Jekyll:** simulated the pipeline in Python — stripped front matter, converted the body with `pandoc -f markdown-raw_tex -t html5 --wrap=none`, substituted the Liquid variables and the `{% if page.strand == 'Culture' %}` conditional, wrote the result, confirmed zero unresolved Liquid tags, and rendered it in headless Chromium. Both strand accents resolved correctly and the raw HTML tables inside the notes survived intact.

## Phase 4 — commit, push, live verification

Two commits, split **along path lines** so no file needed interactive staging and the Jekyll-dependent work is isolated and cleanly revertible:
- `dffd47c` "Fix page structure and spine navigation" — `.gitignore`, `diagrams/**`, `archive/` (16 files)
- `6b366c6` "Publish research notes via Jekyll, link orphaned pages from the index" — `index.html`, `notes/**`, `_layouts/` (8 files)

Pushed `cbe1b83..6b366c6` to `origin/master`. Polled `gh api repos/gregrosser/Yijing-Pathways/pages/builds/latest` until `status=built` **for the exact pushed commit** (took ~5 polls at 10s). Then verified live:
- all 12 index-linked URLs return 200
- note layout applied, both accents correct (`Structure &middot; Note`, `Culture &middot; Note`)
- **`jekyll-relative-links` confirmed active**: `](Group-Table-properties.md)` was rewritten to `href="/Yijing-Pathways/notes/structure/Group-Table-properties.html"` — it handles the baseurl too, so no `_config.yml` was needed
- crawled 47 internal links across 13 live pages — all 200
</work_completed>

<work_remaining>

1. **Item 5 — deduplicate the PDFs.** `collectionPDFs/*.pdf` (19 MB) and `collectionPDFs/view/*.pdf` (18 MB) are the same 13 documents; only `view/` is referenced (verified by grepping every HTML file). Decide which set is canonical and delete the other, updating `index.html`'s 12 `collectionPDFs/view/…` hrefs if `view/` is the one dropped. Note: deleting from the working tree does **not** shrink the 35 MB `.git` — that needs history rewriting, which is a separate decision and would break existing clones.

2. **Item 7 — single source of truth for hexagram data.** `HEXLINES` (64 entries) and `GROUPS` (20 entries) are byte-identical copies in `diagrams/FuXi21.html`, `diagrams/FX_circle_KW_square.html`, `diagrams/kw-square.html`; `FX_TO_KW` is hardcoded in `diagrams/group-table.html` (line ~379 pre-change) but DOM-derived from `data-hex`/`data-kw` attributes in the other two. All four are consistent as of this session (verified). Proposed fix: generate a shared `data/hexagrams.js` from `data/spreadsheets/FX-01.ods` and have all four pages load it. **This subsumes the existing "Rebuild the hexagram Group Table starting from a spreadsheet" TO-DO** in `TO-DOS.md` — do them together.

3. **Mobile responsiveness for the two dense pages.** `diagrams/group-table.html` (+226px) and `diagrams/FX_circle_KW_square.html` (+238px) overflow at phone width. Not a regression — before the viewport tag they were shrunk to fit at 980px — but they now need real responsive work. Note `group-table.html`'s `alignLegendColumns()` uses `getBoundingClientRect()` on `window.load`/`resize`, so any responsive reflow must keep that working.

4. **The public `claude.ai` artifact URLs.** Six references across `notes/structure/Spinal_Mapping.md`, `FX_to_KW.md`, `Group-Table-properties.md` — including one as the subject line of `Group-Table-properties.md` ("Structural qualities of the **FX Group Table** artifact: https://claude.ai/code/artifact/0c3aa836-…"). These are private URLs, now dead ends for public readers. Rewriting the surrounding prose is an editorial call, deliberately left to the user.

5. **Item 9 — `design.md` loose end.** The empty Figma file "PDF Collection Design Reference" (https://www.figma.com/design/ODWz0oFujC0DrgwyMAO7aq) is still undecided: populate as an index linking the 13 book files, or remove and drop the paragraph.

6. **Optional:** `notes/structure/2026-08-13-group-table-artifact-design.md` has front matter and renders live, but is deliberately not linked from `index.html` (reads as an internal working doc). Surface it if wanted.

7. **All prior `TO-DOS.md` items remain untouched** — XianTian circle logic, concentric trigram→hexagram mapping, linking those diagrams, FX/KW trigram circle pairing, yin/yang trigram groups, 3D cube trigrams "à la Z.D. Yung" (still needs the user's source/convention), the central-Taiji digram page (still needs clarification on "FX digrams" vs "KW digrams"), and the KW Square distance markers.
</work_remaining>

<attempted_approaches>

- **`sed` with `&` in the replacement — self-inflicted bug.** `sed 's|Interactive &middot; 10 pages &middot; local|Interactive &middot; 10 pages|'` mangled the line into `Interactive Interactive &middot; 10 pages &middot; localmiddot; 10 pages`, because unescaped `&` in a sed replacement expands to the entire match. Caught by grepping the result instead of trusting the command; fixed with the Edit tool. **The same trap applies to the `sed`-based link fixing used in the previous session** — escape `&` as `\&` or use a different tool.

- **Installing Jekyll locally — failed, do not retry as-is.** `gem install --user-install --no-document jekyll` fails building the `http_parser.rb` native extension: `mkmf.rb can't find header files for ruby`. Needs the `ruby-dev` package, which needs sudo, which this environment can't supply interactively. Ruby 3.3 and pandoc are present; `jekyll`/`bundler` are not. Workaround used: simulate the pipeline with pandoc + manual Liquid substitution (good enough to validate the layout and content, **not** the real build).

- **Wikilink target extension — first attempt was wrong.** Initially converted `[[Group-Table-properties]]` → `[…](Group-Table-properties.html)`. That works on the web but leaves the links **dead inside Obsidian**, breaking graph view and backlinks in the user's daily workflow. Switched all six to `.md` targets, which resolve natively in Obsidian and are rewritten to built URLs by `jekyll-relative-links` (a GitHub Pages default plugin). Confirmed live that the rewrite happens *and* that it prefixes the `/Yijing-Pathways/` baseurl. Alternatives considered and rejected: `permalink:` directory-style URLs (still dead in Obsidian); keeping wikilinks (GitHub Pages has no wikilink support); hand-maintained `.html` twins of each note (recreates the item-7 drift problem).

- **Screenshot comparison without controlling for animation — misleading.** The first pixel-diff run reported `index.html` at 26% changed, which looked like a doctype regression. It was the IntersectionObserver fade-in. `--virtual-time-budget=6000` alone did **not** settle it (still 29%). `--force-prefers-reduced-motion` did, because the page's CSS has a `prefers-reduced-motion` block forcing `opacity: 1` and `animation: none`. **Always pass `--force-prefers-reduced-motion` when diffing screenshots of these pages, and always sanity-check determinism by diffing the same file against itself first.**

- **Splitting commits per logical change — abandoned.** `index.html` carried three distinct changes (head fix, label cleanup + kw-square link, note entries), and interactive staging (`git add -p`) isn't available in this environment. Rather than reconstruct intermediate file states, split the commits along **path boundaries** instead, which kept every file whole and still isolated the risky Jekyll work in `6b366c6`.

- **Playwright MCP** — not attempted this session. The previous session recorded it failing ("Chromium distribution 'chrome' is not found"); system `chromium-browser` via Bash was used throughout instead and worked fine.
</attempted_approaches>

<critical_context>

- **Repo is public and pushing to `master` publishes.** `github.com/gregrosser/Yijing-Pathways`, Pages source = `master` / root, live at `https://gregrosser.github.io/Yijing-Pathways/`. Standing habit (`feedback_push-reminder.md` in memory): check `git status` when a session winds down and *ask* before committing/pushing — never push automatically.

- **The site now depends on Jekyll.** This is new as of `6b366c6`. If a future change breaks the build, the **whole site** fails, not just the notes. Always poll `gh api repos/gregrosser/Yijing-Pathways/pages/builds/latest --jq '.status'` until `built` **and check `.commit` matches the pushed SHA** before declaring anything live. There is deliberately **no `_config.yml` and no `.nojekyll`** — GitHub Pages' defaults are doing the work, including the `jekyll-relative-links` plugin. Adding a malformed `_config.yml` is now a way to break the site.

- **Jekyll conventions in play:** `_layouts/note.html` is the only layout. Notes render at `notes/<dir>/<Name>.html`. Files/dirs beginning with `_` are Jekyll-special. Markdown files **without** front matter are copied verbatim, not rendered. `notes/structure/2026-08-13-…md` is date-prefixed but is *not* treated as a post, because it isn't in `_posts/`.

- **Obsidian ↔ web dual-audience constraint.** These notes are live vault files the user edits daily. Any future link rewriting must keep `.md` relative targets so Obsidian's graph/backlinks keep working; the web side is handled by `jekyll-relative-links`. Do not "fix" these to `.html`.

- **`distance` semantics in `GROUPS`:** `distance == |a-b|/2 + 1`, not `|a-b|`. Worth knowing before touching the FX circle's `buildDistanceLink()` or porting it to `kw-square.html` (the open TO-DO).

- **`group-table.html`'s flip/axis logic still depends on `notes/structure/Group-Table-properties.md`** as its source of truth (`FLIP16_DUAL_ROW`, `groupsForMode`). That note is now *published*, so revising it has both a correctness and a public-content consequence.

- **Headless Chromium in this environment:** `chromium-browser` (snap, v150) works fine reading files directly from `/home/greg/obsidian/vault01/Yijing-Pathways/…` — the snap confinement only blocks the session scratchpad (`/tmp/claude-*`), not the vault, since the vault is under `$HOME`. Useful flags used: `--headless --disable-gpu --no-sandbox --hide-scrollbars --force-prefers-reduced-motion --virtual-time-budget=N --window-size=W,H --screenshot=… --dump-dom`. ImageMagick `compare -metric AE` and Python PIL are available for diffing/cropping; `pandoc` is available; `pip` is **not**, and `python3 -m markdown` is not installed.

- **`index.html` entry cards:** diagram/note entries are `<a class="entry">` wrappers (whole card clickable — a deliberate change from earlier commits `412c868`/`e5b1c10`). PDF entries are `<div class="entry">` with a nested `open →` link. **Never nest an `<a>` inside an `<a class="entry">`** — that's why the notes became their own entries.

- **Note links open in the same tab** (no `target="_blank"`), unlike the diagram entries, because the note layout provides a `← Yijing Pathways` back-link. Intentional.

- **`TO-DOS.md` remains deliberately uncommitted/unpushed** per the user's earlier explicit "local is fine". It was untouched this session. Keep it that way unless asked.

- **`.claude/settings.local.json` is gitignored** (local-only permissions allowlist).
</critical_context>

<current_state>

- **Git:** working tree clean except the intentionally-local `TO-DOS.md`. `master` is pushed and up to date with `origin/master` at `6b366c6`. History: `cbe1b83` → `dffd47c` → `6b366c6`.

- **Live site:** building from `master`/root, build confirmed `built` for `6b366c6`. 47 internal links across 13 pages verified 200. All five reader-facing notes render with the correct strand accents; the sixth (the artifact-design working doc) renders but is unlinked by design.

- **Complete:** review items 1, 2, 3, 4, 6, 8. All verified — by pixel-diff (0 differing pixels across 6 pages), by simulated render, and by live HTTP crawl after the Pages build finished.

- **Not started:** items 5 (duplicate PDFs), 7 (hexagram data single-sourcing), 9 (`design.md` Figma loose end), plus the mobile-responsiveness work on the two dense diagram pages and the decision about the public `claude.ai` artifact URLs.

- **Open questions for the user:** which PDF set is canonical (`collectionPDFs/` vs `collectionPDFs/view/`); whether to rewrite or remove the `claude.ai` artifact references now that the notes are public; whether to surface the artifact-design note on the index; and whether the `.git` history rewrite for size is worth breaking existing clones.

- **No temp files left behind.** All screenshot dirs (`/home/greg/shots`, `/home/greg/yijing-review-shots`), simulated renders (`/home/greg/_sim_*.html`), and probe copies were removed and the removal confirmed.
</current_state>
