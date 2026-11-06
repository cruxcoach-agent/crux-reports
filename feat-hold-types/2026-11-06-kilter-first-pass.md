# Hold types: the first Kilter pass (#63)

*2026-11-06, first version. The labels are not checked against the reference set yet; accuracy follows.*

Every Kilter placement now has a first label in the taxonomy decided for
[#63](https://github.com/CruxCoach/CruxCoach/issues/63) (see the
[taxonomy report](2026-11-06-taxonomy.md)): type, optional second use, size class, direction, foot-only flag, the
measured footprint, and a confidence and a source for each field. This report covers what was labelled, how, how
sure the labels are and what is still open. It shows no hold pictures: the crops come from the board images and stay
internal.

## What was labelled

The current Kilter catalogue has the same 1,191 placements as the geometry bundled in the app.

| Layout | Hold sets | Placements | Labelled | No picture |
|---|---|---:|---:|---:|
| Original | bolt-ons 488, screw-ons 204 | 692 | 641 | 51 |
| Homewall | mainline 234, auxiliary 238, two kickboard sets 27 | 499 | 475 | 24 |
| **All** | | **1,191** | **1,116** | **75** |

**No picture** means the app has no image of that hold:
- The board image of the Original 12 × 14 ends below its top three rows, so 51 holds there have no picture. The
  same gap probably shows in the app's board view for that size.
- At 24 Homewall positions the image shows a round placeholder instead of a hold.

These 75 keep the type "unknown" until a better image or a review fills them in.

## How

1. **Cut out.** Each placement was located on the app's board image with the highest resolution that shows it (7.5
   to 12.3 pixels per inch), checked against the bolt hole, and its outline was cut out.
   - The width and height of the outline give the footprint in centimetres.
   - Where holds touch in the image, the split between them is approximate; those holds are on the review list.
2. **Proposal by rule.** From the footprint and the band that a sloping side leaves in a front view, a rule proposed
   type and direction. Where the screw-ons are concerned, the catalogue's use of the hold broke the tie between foot
   chip and small edge (decision 7: tie-breaker and confidence only).
3. **Checked by eye.** Numbered contact sheets of all holds were checked. About 200 labels were corrected directly
   and about 770 rule proposals were checked and kept. The screw-on sheets (150 holds) are rule only so far.
4. **Hold models.** Matching identical hold models by shape did not separate them reliably at this resolution, so
   every placement was labelled on its own. The Kilter Homewall is not a mirrored hold set: the positions are
   symmetric, the holds are not. The mirror rule therefore applies from Tension on.

## Results

| Type | Original | Homewall | All |
|---|---:|---:|---:|
| Jug (Henkel) | 193 | 202 | 395 |
| Edge (Leiste) | 276 | 183 | 459 |
| Sloper | 27 | 48 | 75 |
| Pinch (Zange) | 9 | 42 | 51 |
| Foot chip (Tritt) | 136 | – | 136 |
| Pocket, volume | – | – | – |
| Unknown (no picture) | 51 | 24 | 75 |

- **Second use** on 230 holds. Most are screw-ons labelled "edge, also a foot chip" or the other way round.
- **Foot only:** 213 holds. These are the screw-ons the catalogue uses almost only as feet, the kickboard sets, and
  the foot rows at the bottom of both layouts.
  - The 68 screw-ons that problems often use as hand holds are labelled edge, with foot chip as their second use.
- **Direction** of the hand holds:
  - 589 down-pull (facing up, up-left or up-right)
  - 68 sidepull
  - 74 undercling
  - 187 all round
- **Size:**
  - Jugs and slopers get a footprint class: small below 12 cm, medium 12 to 17 cm, large above 17 cm.
  - **Edge and pinch size is "unknown" on every Kilter hold:** at this resolution the front view does not show how
    deep an edge is. Per decision 2, edge size stays out of Kilter's stats unless reviews fill it in.

## How sure

| Type confidence | Original | Homewall |
|---|---:|---:|
| High (0.6 and above) | 17 | 0 |
| Medium (0.4 to 0.6) | 581 | 382 |
| Low (below 0.4) | 43 | 93 |

Few labels reach "high". The images are small, and a front view hides the side of a hold that decides between a
flat edge and a jug.

The review list has 619 holds, some for more than one reason:

| Reason | Holds |
|---|---:|
| Direction uncertain | 366 |
| Touches another hold in the image | 263 |
| Type uncertain | 136 |
| No picture | 75 |

**Weak spots:**
- **Direction on the Homewall photos.** The lighting puts a shadow on one side of every hold. That bias is removed
  per image, but the direction is still noisy there.
- **Rounded holds near the edges of the Homewall.** It is hard to tell from the image whether these are slopers or
  blocks to pinch.
- **Edge depth.** It is not visible anywhere on Kilter (see Size).

## Reference set

153 holds, picked at random within each layout and type:

| Layout | Holds | Edge | Jug | Foot chip | Sloper | Pinch |
|---|---:|---:|---:|---:|---:|---:|
| Original | 86 | 30 | 25 | 15 | 10 | 6 |
| Homewall | 67 | 22 | 25 | – | 10 | 10 |

The maintainer checks it, and the accuracy per field (type, second use, direction, foot only) follows in the next
version of this report. The labels were not tuned on these holds after they were picked.

## Next

1. The maintainer's check of the reference set, then accuracy per field and per layout.
2. A proposal for how the dataset reaches the app.
3. A review screen in a test build. It shows a hold highlighted on the board view, its label, and buttons to confirm
   or correct it. It is the way for everyone to check labels without posting hold pictures.
4. Then MoonBoard, Tension and the other boards.
