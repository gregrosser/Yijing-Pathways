---
layout: note
title: "FX Circle Properties"
strand: Structure
---

# FX Circle Properties

Structural qualities of the given FuXi/Xiantian hexagram **circle's own
geometry**, as actually drawn in `../../diagrams/FX_circle_KW_square.html`
(angular position, not FX-number order). This is distinct from the FX
Group Table's row/grouping structure — see `Group-Table-properties.md`
for that — though several findings here connect directly to it
(Observation 10's Klein four-group / cuogua-zonggua work in particular).

## Regeneration method

None of this file depends on memory. All angles are parsed directly from
the SVG, not assumed:

- Parse the 8 `<g transform="rotate\((-?[\d.]+) 500 500\)">` wedge groups
  and all 64 `<g class="glyph" id="glyph-(\d+)">\s*<title>(\S+)\s+(-?[\d.]+)°</title>`
  elements (each hexagram's local angle within its enclosing wedge).
- absolute angle = local angle + enclosing wedge's rotation, mod 360.
- Sort by increasing angle for the counter-clockwise walking order (the
  convention used throughout this file — standard math-angle convention,
  0°=right, 90°=up, increasing = counter-clockwise).
- Cross-reference `HEXLINES` (same file) for each hexagram's line values.
- Outer-trigram names: `<g class="glyph outer" id="glyph-outer-(\d+)">\s*<title>outer (\S+) \(over \d+\)</title>`.

## Observations

### 1. Diametric complements

FX(2k−1) and FX(2k) sit at exactly 180° apart on the circle, for all
k = 1..32, zero exceptions — confirmed directly from raw angle data
(not inferred from line values, unlike the equivalent fact established
from `HEXLINES` alone in `Group-Table-properties.md`). Equivalently:
for every position *p* on the circle, the hexagram at position *p*+32
(mod 64) is the exact line-by-line complement of the hexagram at
position *p*. This is the circle's single most robust property.

### 2. The 8×8 trigram grid

The circle's macro structure is 8 sectors of 45° each, one per **inner**
trigram (lines 1–3), arranged in the canonical Xiantian circle order
(`Qian, Xun, Kan, Gen, Kun, Zhen, Li, Dui` — see Background below). Within
each sector, the 8 members are ordered by ascending FX number, not by an
independent second application of the canonical circle order — the
**outer** trigram's (lines 4–6) sub-order within a sector is inherited
from the pre-existing FX numbering. Confirmed directly: only 2 distinct
8-element outer-trigram sequences occur across all 8 sectors, each the
exact reverse of the other.

### 3. Two-pole complementary unfolding ("barred spiral" structure)

Every hexagram belongs to exactly one FX(2k−1)/FX(2k) pair (Observation
1), so the circle can be read as unfolding simultaneously outward, in
the **same** counter-clockwise direction, from two poles: **FX1** (Qian
over Qian, all six lines yang) and **FX2** (Kun over Kun, all six lines
yin) — the two "pure" hexagrams, diametrically opposite each other.

At every corresponding step *k* along the two arms, the hexagram on
FX2's arm is the **exact line-by-line complement** of the hexagram on
FX1's arm at that same step — not a reversal of reading direction, a
direct term-by-term complementation while both arms move the same way.
This single relationship (already Observation 1, applied position by
position rather than just to the FX1/FX2 pair itself) forces every line
to show the doubling/mirror structure below, confirmed exactly, zero
exceptions, all 6 lines, all 32 steps:

| Line | From FX1's arm | From FX2's arm |
|---|---|---|
| Line 1 | 32 yang | 32 yin |
| Line 2 | 16 yang, 16 yin | 16 yin, 16 yang |
| Line 3 | 2×(8 yang, 8 yin) | 2×(8 yin, 8 yang) |
| Line 4 | 4×(4 yang, 4 yin) | 4×(4 yin, 4 yang) |
| Line 5 | 8×(2 yang, 2 yin) | 8×(2 yin, 2 yang) |
| Line 6 | 16×(yang, yin) | 16×(yin, yang) |

Both columns read outward counter-clockwise from their pole, in the same
rotational direction. Physically this is a 2-fold **rotational** (point)
symmetry — the whole circle maps onto itself under a half-turn combined
with complementation — not a mirror symmetry, matching a real
barred-spiral galaxy's arm structure (two arms trailing the same
rotational sense from opposite ends of a central bar) more precisely
than a mirror-image analogy would.

### 4. Inner trigram = exact 3-bit reflected Gray cycle

Restricting to lines 1–3 (the inner trigram) only, walking the circle
counter-clockwise and aligning to the line-1 boundary: the sequence is
an exact 3-bit **reflected Gray code cycle** — every step (including the
wraparound from the last position back to the first) changes exactly
one line. This is *why* the canonical 8-trigram circle order is what it
is (adjacent trigrams always differ by one line, all the way around).
Confirmed via direct Hamming-distance measurement between all
consecutive trigram values around the cycle.

This does **not** extend to a full 6-bit single-step Gray cycle: measuring
Hamming distance between every pair of geometrically-adjacent
*hexagrams* (all 6 lines) around the full 64-circle gives distance 1 for
only 34 of 64 steps (16 at distance 2, 8 at distance 3, 4 at distance 4,
2 at distance 5, none at distance 6) — a clean halving distribution, but
not a pure single-bit-flip cycle overall. This is a different, stricter
property from Observation 3 above (which holds exactly for all 6 lines) —
the two should not be conflated: Observation 3 is about complementation
between the two arms at matching steps; this is about single-line
adjacency between *consecutive* steps along one direction.

#### Aside: "antipodal Gray codes" — a named match for Observation 4

A quick check found the *standard* textbook reflected binary Gray code
does **not** have the antipodal-complement property in Observation 1/4
(verified directly — neither the plain 3-bit or 6-bit reflected Gray
code has it, nor does any rotation or reversal of the 3-bit version) —
so this circle's inner-trigram structure isn't generic Gray-code
behavior. A web search found the combination is a real, named, actively
studied object: an **(n,t)-antipodal Gray code** (the complement of any
codeword appears exactly *t* steps away in the cycle), originating from
a problem posed by Hunter Snevily, with existence results by Killian and
Savage and a dedicated *Theoretical Computer Science* paper on the
general (n,t) family. This circle's inner-trigram ordering is the
**t = 2ⁿ⁻¹** case (complement at exactly half the cycle — true circular
antipodality): a **(3,4)-antipodal Gray code**.

Low priority / not pursued further yet. Sources:
[Antipodal Gray Codes](https://www.researchgate.net/publication/2536689_Antipodal_Gray_Codes),
[On the (n,t)-antipodal Gray codes — Theoretical Computer Science](https://dl.acm.org/doi/10.1016/j.tcs.2006.12.005),
[Antipodal Gray codes — ScienceDirect](https://www.sciencedirect.com/science/article/pii/S0012365X03006563),
[Combinatorial Gray codes — an updated survey (Mütze)](https://www.combinatorics.org/files/Surveys/ds26/ds26v1-2023.pdf).

## Background

The Xiantian trigram circle order referenced above:
[Qian, Xun, Kan, Gen, Kun, Zhen, Li, Dui] at
[90, 45, 0, 315, 270, 225, 180, 135] degrees — same order documented in
`Group-Table-properties.md`'s own Background section.

## Related

- `Group-Table-properties.md` Observation 10 (Klein four-group orbits
  under cuogua/zonggua) — the same complement (cuogua) and reversal
  (zonggua) operations underlie this file's Observations 1 and 3.
- `Group-Table-properties.md` Observation 11 (binary-sequence numbering
  comparison) — a different question (which *numbering* fits which
  relation), not to be conflated with this file's focus on the given
  circle's own geometry independent of numbering.
