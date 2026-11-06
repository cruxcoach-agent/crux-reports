# Hold types: the first Kilter pass (#63)

*2026-11-06, second version: lossless board images, the 24 Homewall holds that only showed a placeholder are
labelled, and "foot chip" is no longer a second use. The labels are not checked against the reference set yet;
accuracy follows from the review in a test build.*

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
| Homewall | mainline 234, auxiliary 238, two kickboard sets 27 | 499 | 499 | 0 |
| **All** | | **1,191** | **1,140** | **51** |

**No picture:** the board image of the Original 12 × 14 ends below its top three rows, in the official app as well,
so 51 holds there have no picture. They stay "unknown".

**Images.** Kilter's old image server no longer serves images, and there are no larger versions than the
1,080-pixel ones. The lossless originals of the same size were used instead of the app's re-encoded copies. For the
Homewall 10 × 12 they show real holds at 24 positions where the app's copy shows a placeholder disc; those 24 are
labelled now. The app's own copy of that image is unchanged.

## How

1. **Cut out.** Each placement was located on the board image with the highest resolution that shows it (7.5 to
   12.3 pixels per inch), checked against the bolt hole, and its outline was cut out.
   - The width and height of the outline give the footprint in centimetres.
   - Where holds touch in the image, the split between them is approximate; those holds are on the review list.
2. **Proposal by rule.** From the footprint and the band that a sloping side leaves in a front view, a rule proposed
   type and direction. Where the screw-ons are concerned, the catalogue's use of the hold broke the tie between foot
   chip and small edge (decision 7: tie-breaker and confidence only).
3. **Checked by eye.** Numbered contact sheets of all holds were checked. About 210 labels were corrected directly
   and about 780 rule proposals were checked and kept. The screw-on sheets (150 holds) are rule only so far.
4. **Hold models.** Matching identical hold models by shape did not separate them reliably at this resolution, so
   every placement was labelled on its own. The Kilter Homewall is not a mirrored hold set: the positions are
   symmetric, the holds are not. The mirror rule therefore applies from Tension on.

## Results

| Type | Original | Homewall | All |
|---|---:|---:|---:|
| Jug (Henkel) | 194 | 206 | 400 |
| Edge (Leiste) | 275 | 200 | 475 |
| Sloper | 27 | 51 | 78 |
| Pinch (Zange) | 9 | 42 | 51 |
| Foot chip (Tritt) | 136 | – | 136 |
| Pocket, volume | – | – | – |
| Unknown (no picture) | 51 | – | 51 |

- **Second use** on 26 holds, all real second grips (for example a jug that is also a sloper). Whether a hold is for
  hands or for feet only is the foot-only field, never a second use.
- **Foot only:** 213 holds. These are the screw-ons the catalogue uses almost only as feet, the kickboard sets, and
  the foot rows at the bottom of both layouts.
  - The 68 screw-ons that problems often use as hand holds are labelled edge and are not foot only.
- **Direction** of the hand holds:
  - 605 down-pull (facing up, up-left or up-right)
  - 58 sidepull
  - 57 undercling
  - 207 all round
- **Size:**
  - Jugs and slopers get a footprint class: small below 12 cm, medium 12 to 17 cm, large above 17 cm.
  - **Edge and pinch size is "unknown" on every Kilter hold:** at this resolution the front view does not show how
    deep an edge is. Per decision 2, edge size stays out of Kilter's stats unless reviews fill it in.

## How sure

| Type confidence | Original | Homewall |
|---|---:|---:|
| High (0.6 and above) | 17 | 0 |
| Medium (0.4 to 0.6) | 581 | 403 |
| Low (below 0.4) | 43 | 96 |

Few labels reach "high". The images are small, and a front view hides the side of a hold that decides between a
flat edge and a jug.

The review list has 600 holds, some for more than one reason:

| Reason | Holds |
|---|---:|
| Direction uncertain | 392 |
| Touches another hold in the image | 247 |
| Type uncertain | 139 |
| No picture | 51 |

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

The maintainer checks it in two rounds, in a review screen of a test build:
1. **Blind.** Type, direction and foot only are answered before the computed label is shown; each may be "can't
   tell".
2. **Decide.** Only the disagreements are shown, and the maintainer decides who was right.

The report will give both numbers: agreement in the blind round, and after the second round how often each side was
wrong. The labels were not tuned on these holds after they were picked.

## Next

1. The maintainer's check of the reference set, then accuracy per field and per layout.
2. A proposal for how the dataset reaches the app.
3. The review screen in a test build (in progress): it shows the hold on the board view and close up, asks first and
   shows the computed label afterwards. It is the way for everyone to check labels without posting hold pictures.
4. Then MoonBoard, Tension and the other boards.
