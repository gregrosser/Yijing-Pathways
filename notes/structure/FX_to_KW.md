# FX to KW

Correspondence between this project's own hexagram numbering (FX_01–FX_64)
and the traditional King Wen sequence (KW_01–KW_64), plus what the
correspondence reveals about how the two sequences are built.

Live data: `spreadsheets/FX-01.ods`, tables T3 (`A13:J22`, the KW-number
mirror of T1), T4 (`L13:O22`, KW-group sums) and T5 (`Q13:T22`, FX+KW sums
combined) — all cross-checked against this document with zero
discrepancies. See also [[Group-Table-properties]] and [[Spinal_Mapping]]
for the FX-side structure this builds on.

## Overview

1. The correspondence table
2. Verification method
3. KW's own pairing structure
4. FX quartets vs KW: the cross-cut

## 1. The correspondence table

<div style="display:flex; justify-content:center; gap:1.5em;">

<table style="border-collapse:collapse;">
<tr><th style="border:1px solid #888; padding:3px 8px;">FX</th><th style="border:1px solid #888; padding:3px 8px;">KW</th></tr>
<tr><td style="border:1px solid #888; padding:3px 8px; text-align:center;">01</td><td style="border:1px solid #888; padding:3px 8px; text-align:center;">01</td></tr>
<tr><td style="border:1px solid #888; padding:3px 8px; text-align:center;">02</td><td style="border:1px solid #888; padding:3px 8px; text-align:center;">02</td></tr>
<tr><td style="border:1px solid #888; padding:3px 8px; text-align:center;">03</td><td style="border:1px solid #888; padding:3px 8px; text-align:center;">43</td></tr>
<tr><td style="border:1px solid #888; padding:3px 8px; text-align:center;">04</td><td style="border:1px solid #888; padding:3px 8px; text-align:center;">23</td></tr>
<tr><td style="border:1px solid #888; padding:3px 8px; text-align:center;">05</td><td style="border:1px solid #888; padding:3px 8px; text-align:center;">14</td></tr>
<tr><td style="border:1px solid #888; padding:3px 8px; text-align:center;">06</td><td style="border:1px solid #888; padding:3px 8px; text-align:center;">08</td></tr>
<tr><td style="border:1px solid #888; padding:3px 8px; text-align:center;">07</td><td style="border:1px solid #888; padding:3px 8px; text-align:center;">34</td></tr>
<tr><td style="border:1px solid #888; padding:3px 8px; text-align:center;">08</td><td style="border:1px solid #888; padding:3px 8px; text-align:center;">20</td></tr>
<tr><td style="border:1px solid #888; padding:3px 8px; text-align:center;">09</td><td style="border:1px solid #888; padding:3px 8px; text-align:center;">09</td></tr>
<tr><td style="border:1px solid #888; padding:3px 8px; text-align:center;">10</td><td style="border:1px solid #888; padding:3px 8px; text-align:center;">16</td></tr>
<tr><td style="border:1px solid #888; padding:3px 8px; text-align:center;">11</td><td style="border:1px solid #888; padding:3px 8px; text-align:center;">05</td></tr>
<tr><td style="border:1px solid #888; padding:3px 8px; text-align:center;">12</td><td style="border:1px solid #888; padding:3px 8px; text-align:center;">35</td></tr>
<tr><td style="border:1px solid #888; padding:3px 8px; text-align:center;">13</td><td style="border:1px solid #888; padding:3px 8px; text-align:center;">26</td></tr>
<tr><td style="border:1px solid #888; padding:3px 8px; text-align:center;">14</td><td style="border:1px solid #888; padding:3px 8px; text-align:center;">45</td></tr>
<tr><td style="border:1px solid #888; padding:3px 8px; text-align:center;">15</td><td style="border:1px solid #888; padding:3px 8px; text-align:center;">11</td></tr>
<tr><td style="border:1px solid #888; padding:3px 8px; text-align:center;">16</td><td style="border:1px solid #888; padding:3px 8px; text-align:center;">12</td></tr>
</table>

<table style="border-collapse:collapse;">
<tr><th style="border:1px solid #888; padding:3px 8px;">FX</th><th style="border:1px solid #888; padding:3px 8px;">KW</th></tr>
<tr><td style="border:1px solid #888; padding:3px 8px; text-align:center;">17</td><td style="border:1px solid #888; padding:3px 8px; text-align:center;">10</td></tr>
<tr><td style="border:1px solid #888; padding:3px 8px; text-align:center;">18</td><td style="border:1px solid #888; padding:3px 8px; text-align:center;">15</td></tr>
<tr><td style="border:1px solid #888; padding:3px 8px; text-align:center;">19</td><td style="border:1px solid #888; padding:3px 8px; text-align:center;">58</td></tr>
<tr><td style="border:1px solid #888; padding:3px 8px; text-align:center;">20</td><td style="border:1px solid #888; padding:3px 8px; text-align:center;">52</td></tr>
<tr><td style="border:1px solid #888; padding:3px 8px; text-align:center;">21</td><td style="border:1px solid #888; padding:3px 8px; text-align:center;">38</td></tr>
<tr><td style="border:1px solid #888; padding:3px 8px; text-align:center;">22</td><td style="border:1px solid #888; padding:3px 8px; text-align:center;">39</td></tr>
<tr><td style="border:1px solid #888; padding:3px 8px; text-align:center;">23</td><td style="border:1px solid #888; padding:3px 8px; text-align:center;">54</td></tr>
<tr><td style="border:1px solid #888; padding:3px 8px; text-align:center;">24</td><td style="border:1px solid #888; padding:3px 8px; text-align:center;">53</td></tr>
<tr><td style="border:1px solid #888; padding:3px 8px; text-align:center;">25</td><td style="border:1px solid #888; padding:3px 8px; text-align:center;">61</td></tr>
<tr><td style="border:1px solid #888; padding:3px 8px; text-align:center;">26</td><td style="border:1px solid #888; padding:3px 8px; text-align:center;">62</td></tr>
<tr><td style="border:1px solid #888; padding:3px 8px; text-align:center;">27</td><td style="border:1px solid #888; padding:3px 8px; text-align:center;">60</td></tr>
<tr><td style="border:1px solid #888; padding:3px 8px; text-align:center;">28</td><td style="border:1px solid #888; padding:3px 8px; text-align:center;">56</td></tr>
<tr><td style="border:1px solid #888; padding:3px 8px; text-align:center;">29</td><td style="border:1px solid #888; padding:3px 8px; text-align:center;">41</td></tr>
<tr><td style="border:1px solid #888; padding:3px 8px; text-align:center;">30</td><td style="border:1px solid #888; padding:3px 8px; text-align:center;">31</td></tr>
<tr><td style="border:1px solid #888; padding:3px 8px; text-align:center;">31</td><td style="border:1px solid #888; padding:3px 8px; text-align:center;">19</td></tr>
<tr><td style="border:1px solid #888; padding:3px 8px; text-align:center;">32</td><td style="border:1px solid #888; padding:3px 8px; text-align:center;">33</td></tr>
</table>

<table style="border-collapse:collapse;">
<tr><th style="border:1px solid #888; padding:3px 8px;">FX</th><th style="border:1px solid #888; padding:3px 8px;">KW</th></tr>
<tr><td style="border:1px solid #888; padding:3px 8px; text-align:center;">33</td><td style="border:1px solid #888; padding:3px 8px; text-align:center;">13</td></tr>
<tr><td style="border:1px solid #888; padding:3px 8px; text-align:center;">34</td><td style="border:1px solid #888; padding:3px 8px; text-align:center;">07</td></tr>
<tr><td style="border:1px solid #888; padding:3px 8px; text-align:center;">35</td><td style="border:1px solid #888; padding:3px 8px; text-align:center;">49</td></tr>
<tr><td style="border:1px solid #888; padding:3px 8px; text-align:center;">36</td><td style="border:1px solid #888; padding:3px 8px; text-align:center;">04</td></tr>
<tr><td style="border:1px solid #888; padding:3px 8px; text-align:center;">37</td><td style="border:1px solid #888; padding:3px 8px; text-align:center;">30</td></tr>
<tr><td style="border:1px solid #888; padding:3px 8px; text-align:center;">38</td><td style="border:1px solid #888; padding:3px 8px; text-align:center;">29</td></tr>
<tr><td style="border:1px solid #888; padding:3px 8px; text-align:center;">39</td><td style="border:1px solid #888; padding:3px 8px; text-align:center;">55</td></tr>
<tr><td style="border:1px solid #888; padding:3px 8px; text-align:center;">40</td><td style="border:1px solid #888; padding:3px 8px; text-align:center;">59</td></tr>
<tr><td style="border:1px solid #888; padding:3px 8px; text-align:center;">41</td><td style="border:1px solid #888; padding:3px 8px; text-align:center;">37</td></tr>
<tr><td style="border:1px solid #888; padding:3px 8px; text-align:center;">42</td><td style="border:1px solid #888; padding:3px 8px; text-align:center;">40</td></tr>
<tr><td style="border:1px solid #888; padding:3px 8px; text-align:center;">43</td><td style="border:1px solid #888; padding:3px 8px; text-align:center;">63</td></tr>
<tr><td style="border:1px solid #888; padding:3px 8px; text-align:center;">44</td><td style="border:1px solid #888; padding:3px 8px; text-align:center;">64</td></tr>
<tr><td style="border:1px solid #888; padding:3px 8px; text-align:center;">45</td><td style="border:1px solid #888; padding:3px 8px; text-align:center;">22</td></tr>
<tr><td style="border:1px solid #888; padding:3px 8px; text-align:center;">46</td><td style="border:1px solid #888; padding:3px 8px; text-align:center;">47</td></tr>
<tr><td style="border:1px solid #888; padding:3px 8px; text-align:center;">47</td><td style="border:1px solid #888; padding:3px 8px; text-align:center;">36</td></tr>
<tr><td style="border:1px solid #888; padding:3px 8px; text-align:center;">48</td><td style="border:1px solid #888; padding:3px 8px; text-align:center;">06</td></tr>
</table>

<table style="border-collapse:collapse;">
<tr><th style="border:1px solid #888; padding:3px 8px;">FX</th><th style="border:1px solid #888; padding:3px 8px;">KW</th></tr>
<tr><td style="border:1px solid #888; padding:3px 8px; text-align:center;">49</td><td style="border:1px solid #888; padding:3px 8px; text-align:center;">25</td></tr>
<tr><td style="border:1px solid #888; padding:3px 8px; text-align:center;">50</td><td style="border:1px solid #888; padding:3px 8px; text-align:center;">46</td></tr>
<tr><td style="border:1px solid #888; padding:3px 8px; text-align:center;">51</td><td style="border:1px solid #888; padding:3px 8px; text-align:center;">17</td></tr>
<tr><td style="border:1px solid #888; padding:3px 8px; text-align:center;">52</td><td style="border:1px solid #888; padding:3px 8px; text-align:center;">18</td></tr>
<tr><td style="border:1px solid #888; padding:3px 8px; text-align:center;">53</td><td style="border:1px solid #888; padding:3px 8px; text-align:center;">21</td></tr>
<tr><td style="border:1px solid #888; padding:3px 8px; text-align:center;">54</td><td style="border:1px solid #888; padding:3px 8px; text-align:center;">48</td></tr>
<tr><td style="border:1px solid #888; padding:3px 8px; text-align:center;">55</td><td style="border:1px solid #888; padding:3px 8px; text-align:center;">51</td></tr>
<tr><td style="border:1px solid #888; padding:3px 8px; text-align:center;">56</td><td style="border:1px solid #888; padding:3px 8px; text-align:center;">57</td></tr>
<tr><td style="border:1px solid #888; padding:3px 8px; text-align:center;">57</td><td style="border:1px solid #888; padding:3px 8px; text-align:center;">42</td></tr>
<tr><td style="border:1px solid #888; padding:3px 8px; text-align:center;">58</td><td style="border:1px solid #888; padding:3px 8px; text-align:center;">32</td></tr>
<tr><td style="border:1px solid #888; padding:3px 8px; text-align:center;">59</td><td style="border:1px solid #888; padding:3px 8px; text-align:center;">03</td></tr>
<tr><td style="border:1px solid #888; padding:3px 8px; text-align:center;">60</td><td style="border:1px solid #888; padding:3px 8px; text-align:center;">50</td></tr>
<tr><td style="border:1px solid #888; padding:3px 8px; text-align:center;">61</td><td style="border:1px solid #888; padding:3px 8px; text-align:center;">27</td></tr>
<tr><td style="border:1px solid #888; padding:3px 8px; text-align:center;">62</td><td style="border:1px solid #888; padding:3px 8px; text-align:center;">28</td></tr>
<tr><td style="border:1px solid #888; padding:3px 8px; text-align:center;">63</td><td style="border:1px solid #888; padding:3px 8px; text-align:center;">24</td></tr>
<tr><td style="border:1px solid #888; padding:3px 8px; text-align:center;">64</td><td style="border:1px solid #888; padding:3px 8px; text-align:center;">44</td></tr>
</table>

</div>

## 2. Verification method

- **FX ground truth**: each FX_NN's 6-line pattern, parsed directly from
  the SVG glyphs in the `fx_group_table.html` artifact (source:
  https://claude.ai/code/artifact/0c3aa836-a82e-4bde-b072-b9a87ecbf557),
  encoded bottom-up (line1..line6, 1=yang/0=yin). All 64 patterns
  confirmed distinct.
- **KW ground truth**: the classical lower-trigram × upper-trigram matrix
  (Fu Xi bagua order: Qian, Dui, Li, Zhen, Xun, Kan, Gen, Kun) that
  generates the King Wen sequence. Not re-derived from any project
  artifact — this is the standard reference table. Trigram bits: Qian 111,
  Dui 110, Li 101, Zhen 100, Xun 011, Kan 010, Gen 001, Kun 000; hexagram
  bits = lower-trigram bits + upper-trigram bits (lines 1–3, then 4–6).
- **Cross-check before trusting**: matched against three hand-supplied
  anchors before anything else was computed — FX_01=KW_01, FX_02=KW_02,
  FX_03=KW_43 — all three matched exactly against the matrix above before
  it was used for the remaining 61.
- **Result**: a clean bijection. 64 distinct FX bit-patterns, 64 distinct
  KW slots, zero collisions, zero leftovers.

## 3. KW's own pairing structure

The King Wen sequence is predominantly made of consecutive **inverse**
(zong) pairs — that's the sequence's defining design, not an
approximation of it. Checked directly against the matrix in §2:

- Exactly **8** KW hexagrams satisfy `inv(n) = n` (self-inverse under
  line-reversal): **1, 2, 27, 28, 29, 30, 61, 62**. This has to be exactly
  8 — a palindromic hexagram is fixed by 3 independent line-pair choices
  ({1,6},{2,5},{3,4}), 2³ = 8 — and complement has no fixed points, so
  these 8 split cleanly into 4 complement pairs.
- All four complement pairs are consecutive: **(1,2), (27,28), (29,30),
  (61,62)**. Zero exceptions. These are exactly the four pairs sitting in
  `FX-01.ods` T3, rows 16–19, columns C/D.
- The other 56 hexagrams pair by reversal into 28 zong-pairs — also
  checked exhaustively: **all 28 are consecutive**, zero exceptions.

So all 32 pairs in the King Wen sequence are consecutive-numbered — 28 by
reversal (the predominant, defining mechanism) and 4 by complement (the
only available fallback for the 8 hexagrams reversal can't pair). The
fallback exists because reversal has literally nothing to pair those 8
with; that it also preserves numeric adjacency is a separate design
choice, not a mathematical necessity.

## 4. FX quartets vs KW: the cross-cut

Every FX quartet is a Klein-four-group orbit under the two symmetries —
`{n, zong(n), cuo(n), zong(cuo(n))}` — and splits into two pairs two
different ways: by complement, or by reversal. FX and KW numbering each
make a *different* one of these splits visible.

**Example** (the one that prompted this check): FX{9,10,17,18} and
KW{9,10,15,16} are the same 4 hexagrams. FX's own complement-consecutive
design pairs them as {9,10} and {17,18}. But the KW-consecutive pairing
is a *different* split of the same quartet — {FX_09,FX_17} and
{FX_10,FX_18} — and those are zong-pairs, not the FX-adjacent pairs.

Checked against all 12 quartets, both axes, zero exceptions: the FX-side
pairing is always the complement-split; the KW-consecutive pairing is
always the *zong*-split of that same quartet, cutting across the FX
split rather than reproducing it.

| FX quartet | FX cuo-pairs | KW-consecutive pairs (= FX zong-pairs) |
|---|---|---|
| {9,10,17,18} | (9,10) (17,18) | (FX9,FX17) (FX18,FX10) |
| {5,6,33,34} | (5,6) (33,34) | (FX34,FX6) (FX33,FX5) |
| {13,14,49,50} | (13,14) (49,50) | (FX49,FX13) (FX14,FX50) |
| {7,8,31,32} | (7,8) (31,32) | (FX31,FX8) (FX32,FX7) |
| {11,12,47,48} | (11,12) (47,48) | (FX11,FX48) (FX12,FX47) |
| {3,4,63,64} | (3,4) (63,64) | (FX4,FX63) (FX3,FX64) |
| {21,22,41,42} | (21,22) (41,42) | (FX41,FX21) (FX22,FX42) |
| {29,30,57,58} | (29,30) (57,58) | (FX30,FX58) (FX29,FX57) |
| {45,46,53,54} | (45,46) (53,54) | (FX53,FX45) (FX46,FX54) |
| {27,28,39,40} | (27,28) (39,40) | (FX39,FX28) (FX40,FX27) |
| {19,20,55,56} | (19,20) (55,56) | (FX55,FX20) (FX56,FX19) |
| {35,36,59,60} | (35,36) (59,60) | (FX59,FX36) (FX35,FX60) |

So FX and KW numbering are, in a precise and fully verified sense,
orthogonal readings of the same underlying Klein-four structure: FX makes
complement-adjacency legible; KW makes reversal-adjacency legible — for
the very same set of quartets.

## Position (interpretive, not proven)

The author's working theory — explicitly a gut feeling, not a claim
resting on the above math — is that FX predates KW: a long-lived,
sophisticated FX-based interpretive culture, later giving rise to a
breakaway "humanitarian" reordering (KW) at the Zhou cultural shift, with
FX's power/logic-based structure recast into KW's more human, interwoven
one. See [[Fuxi-sequence-origins]] for the fuller antiquity/elite-secrecy
framing this extends.

The one honest resonance worth naming: KW's structure isn't
self-sufficient. For 56 hexagrams it runs on its own logic (reversal);
for the 8 where reversal gives nothing, it falls back to complement — the
operation FX numbers consecutively everywhere. So KW, exactly at the
point its own logic runs out, quietly depends on the older operation to
complete itself. Whether that reflects real history or is just how a
fixed-point-free group action has to shake out regardless of who built
what when — the structure alone can't say.
