---
layout: note
title: "Spinal Mapping"
strand: Structure
---

# Spinal Mapping

The **FX Spine** artifacts (two axis variants), imported locally so they
don't depend solely on the claude.ai-hosted copies:
- FX_spine_axis_31_32 — [local copy](../../archive/old-architecture/FX_spine_axis_31_32.html) · [claude.ai artifact](https://claude.ai/code/artifact/9c879d6c-a1b4-49f2-a8d5-b8599f7d6a08)
- FX_spine_axis_33_34 — [local copy](../../archive/old-architecture/FX_spine_axis_33_34.html) · [claude.ai artifact](https://claude.ai/code/artifact/26ebb7d6-cf9f-4c2a-a4c6-6e3ee3df7fb2)

Both render the same underlying 64-row table (identical data, identical
pairing); they differ only in which axis's six quartets get ribbon overlays
drawn across the spine. Companion artifact, source of the FX numbering and
the quartet/pair groupings referenced below: the **FX Group Table** —
https://claude.ai/code/artifact/0c3aa836-a82e-4bde-b072-b9a87ecbf557
(documented in full in [Group Table Properties](Group-Table-properties.md)).

## Overview

1. What the spine shows
2. Verification
3. Relationship to the FX Group Table
4. Shifted Inverse Overlay

### 1. What the spine shows

A vertical column of 64 rows. Row *n* pairs {zōng(*n*), *n*} — *n* counts
sequentially 1 to 64 down the right side, and its **zōng** partner (the
hexagram obtained by reversing the line order top-to-bottom — line 1
becomes line 6, line 2 becomes line 5, and so on) sits at the same row on
the left. The 8 self-inverse hexagrams (zōng(*n*) = *n*, i.e. the hexagram
is unchanged by reversal) are highlighted; every other row's left-side
partner reappears later in the spine at its own row, with the pair
reversed — e.g. row 3 shows {64, 3} and row 64 shows {3, 64}.

Each axis variant additionally draws ribbon overlays linking the three
zōng-dual pairs that make up each of that axis's six quartets (see
[Group Table Properties](Group-Table-properties.md) Observation 2 for the quartet structure itself).
The 31/32-axis file scales its ribbons 30% narrower than the 33/34-axis
file and uses a different reference quartet (FX{13,14,49,50}, the largest
span on that axis, distance 19) — a cosmetic choice, not a structural one.


### 2. Verification

Checked computationally (2026-08-09), not by eye: the actual per-hexagram
line data was parsed directly out of the FX Group Table artifact's
embedded SVGs (64 six-line glyphs, one per FX number), zōng(*n*) was
computed for all 64 FX numbers from that data by reversing each line
sequence and matching against the other 63 patterns, and every claim in
both spine artifacts was checked against the result.

- All 64 row pairs {zōng(n), n} shown in both artifacts match the computed
  reversal exactly — zero errors.
- The 8 self-inverse hexagrams are exactly the fixed points of zōng.
- All 12 quartet ribbon groupings (6 per axis file) match the FX Group
  Table's quartets exactly, and each one's claimed inner/outer zōng-pair
  assignment checks out with no mismatches.
- All distance annotations in the ribbon-drawing code comments (13, 19,
  31, 7, 15, 11, 5) match the FX Group Table's `dist` column exactly.

### 3. Relationship to the FX Group Table

The spine is a second rendering of the same zōng structure documented as
**Observation 2 (Lateral symmetry)** in [Group Table Properties](Group-Table-properties.md) — that
document derives the row-(11−*n*) quartet-matching pattern from the group
table's own layout; this one lays all 64 hexagrams out as a single ordered
column and draws the zōng pairing directly, rather than reading it off two
side-by-side axis tables. The two documents describe the same underlying
fact from different vantage points and should be read together.

### 4. Shifted Inverse Overlay

Observed directly from the rendered `FX_spine_axis_33_34.html` picture
(2026-08-09): take an exact copy of the image, rotate it 180°, and
translate the copy vertically by exactly one pair (2 rows). The rotated,
shifted copy's ribbons land on exactly the same rows as the original's.

**Why.** Treat the six ribboned quartets as a set of row-positions only,
ignoring for a moment which numbers sit in them:

```
S = {3,4, 7,8, 11,12, 19,20, 27,28, 31,32, 35,36, 39,40, 47,48, 55,56, 59,60, 63,64}
```

A plain 180° rotation of the image reflects row-position *p* through the
picture's own geometric centre, mapping *p* ↔ (65−*p*) — pivot 32.5,
exactly midway down all 64 rows. That map does *not* carry *S* onto
itself. Shift the rotated copy down by one further pair, and the
combined map becomes *p* ↔ (67−*p*) — pivot 33.5, i.e. the seam between
rows 33 and 34. Checked against all twelve pairs in *S*, this holds with
zero exceptions: 3↔64, 4↔63, 7↔60, 8↔59, 11↔56, 12↔55, 19↔48, 20↔47,
27↔40, 28↔39, 31↔36, 32↔35.

So the one-pair shift isn't an arbitrary fudge — it's exactly the
correction needed to move the rotation's pivot from the *middle of the
picture* (32.5) to the *middle of rows 33/34* (33.5), which is the axis
pair the file is named for. The title's claim is true in a literal,
geometric sense: this picture has 180° rotational symmetry centred on
FX(33,34) itself, one row below its own visual centre.

**By distance.** Grouping those twelve pairs back into their parent
quartets (labelled by the `dist` circle each carries in the FX Group
Table) shows the transform doesn't just preserve the row-set *S* in the
aggregate — it maps each quartet onto a specific, single partner:

- The two **dist-13** quartets, {7,8,31,32} and {35,36,59,60}, map
  **onto each other** — every row of one lands on a row of the other
  (7↔60, 8↔59, 31↔36, 32↔35).
- The two **dist-19** quartets, {11,12,47,48} and {19,20,55,56}, map
  **onto each other** the same way (11↔56, 12↔55, 47↔20, 48↔19).
- The **dist-7** quartet, {27,28,39,40}, maps **onto itself**
  (27↔40, 28↔39) — it doesn't pair with another quartet, it's fixed by
  the transform.
- The **dist-31** quartet, {3,4,63,64}, likewise maps **onto itself**
  (3↔64, 4↔63) — also fixed.

So of the six quartets, four (the matched dist-13 and dist-19 pairs) swap
places under Shifted Inverse Overlay, and two (dist-7 and dist-31) are
individually self-symmetric — each already occupies a rotationally
symmetric position on its own.

**Caveat — positional, not fully numeric.** This exact overlay is a fact
about *where the ribbons are drawn* (row positions), not about the
numbers written inside them. A 180° rotation also swaps left↔right, so
for the displayed *numbers* to overlay too would additionally require
zōng(*p*) = 67−*p* for every ribboned row. That only holds for the two quartets whose internal sum is exactly
67 — {3,4,63,64} and {27,28,39,40}. The other four quartets (internal
sums 59, 75, 39, 95 respectively for {11,12,47,48}, {19,20,55,56},
{7,8,31,32}, {35,36,59,60}) return to the same rows under
rotate-and-shift, but display different numbers there. "Shifted Inverse
Overlay" is a structural/positional symmetry of the whole picture; it is
a numeric palindrome only for those two quartets.

**Axis-specific.** Checked against `FX_spine_axis_31_32.html` the same
way: it does not hold there. That file's quartet-pair sums (62/64, 26/28,
38/40, 98/100, 86/88 — outer and inner differing by a constant +2 rather
than being equal) don't average to 31+32=63 or satisfy any comparable
*p* ↔ (const−*p*) identity across all six quartets. Shifted Inverse
Overlay is a real, distinguishing property of the 33/34-axis rendering,
not a general fact about the spine.

**A note — 33/11 = 3.** 33 pairs — one pair more
than the 64 hexagrams (32 pairs) actually give. Separately, the
pair-groups FX(23,24) and FX(43,44) are also linked
by this same transform (67−23=44, 67−24=43), and the distance between
them — measured the same way the quartet distances above are (an
inclusive count of pair-slots, out of the spine's 32, running from one
group to the other) — is 22−12+1 = **11**. 33/11 = **3** exactly.

