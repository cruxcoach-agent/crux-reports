# Hold types: every board, a check screen, and the first stats to choose from (#63)

*2026-11-07, night pass. None of these labels has been checked against a reference set yet. The Kilter blind round
in the test build will give the first measured accuracy.*

Since the [first Kilter pass](2026-11-06-kilter-first-pass.md), the other boards have their first labels too. They
use the same taxonomy and fields as Kilter (see the [taxonomy report](2026-11-06-taxonomy.md)): type, optional
second grip, size class, direction, a foot-only flag, the measured footprint, and a confidence and a source for every
field. Test builds also have a second review screen now, for checking the labels of any board. This report shows no
hold pictures: the crops come from the board images and stay internal.

## Coverage

Every placement in the app's bundled geometry was looked at. On every board the bundled geometry is the same as the
current catalogue.

| Board | Placements | Typed | Direction only | Unknown | Why unknown |
|---|---:|---:|---:|---:|---|
| Kilter (Original, Homewall) | 1,191 | 1,140 | – | 51 | the top three rows of the Original 12 × 14 image are missing |
| MoonBoard (all 7 generations) | 1,022 | 1,022 | – | 0 | |
| Tension (Board 1, Board 2 Mirror, Board 2 Spray) | 1,683 | 1,299 | – | 384 | two hold sets of the wider Board 2 versions are in no board image; they appear in under 0.2 % of hold uses |
| Grasshopper | 466 | 466 | – | 0 | |
| Decoy (two layouts) | 1,036 | 454 | 2 | 580 | the image of layout 1 shows placeholder discs (578); 2 holds are not in any image |
| So iLL | 340 | 0 | 235 | 105 | the board image is a drawing: it shows outlines and often the rim, not the kind of grip |
| Touchstone | 648 | – | – | 648 | the board image shows flat outlines only |
| Shiny Wall | 2,042 | – | – | 2,042 | the board images show flat outlines only |
| **All** | **8,428** | **4,381** | **237** | **3,810** | |

Shiny Wall's placements overlap between its five wall sizes, so it has fewer physical holds than placements.

## How the labels were made

1. **Cut out.** Each hold was located on the app's own board image that shows it best, from the placement
   coordinates (Aurora boards) or from the app's MoonBoard hold map (MoonBoard). Its outline gives the footprint.
   Where the outline was not found, the label still comes from the picture, without a footprint.
2. **Labelled by eye.** Numbered contact sheets per board, with a short written guide per board, one line per hold:
   type, second grip, size, direction, a confidence for type and direction, and a note on what the picture shows.
3. **Mirror rule.** Where a board is a mirrored hold set, a hold whose picture matches its partner's when flipped
   (a correlation of at least 0.8) gets the partner's label with left and right swapped and a lower confidence
   (factor 0.9). Its source says "mirrored". That covers 616 typed holds on the Tension Board 2 Mirror, Grasshopper and
   Decoy, plus 160 So iLL directions. The Tension Board 2 Spray is not mirrored, and at the same positions it carries
   other holds than the Mirror, so all of its holds were labelled on their own.
4. **Foot only** follows the Kilter rule: the set's default role is foot, and the catalogue uses the hold as a
   foot hold at least 90 % of the time (decision 7, tie-breaker only). MoonBoard has no foot-only sets.
5. **Edge size** stays unknown nearly everywhere. Front views don't show edge depth, so per decision 2 no board's stats
   will show edge size yet.

| Board | Picture | Type confidence (high / medium / low) | Direction confidence (high / medium / low) | Review list |
|---|---|---|---|---:|
| Kilter | renders (Original), photos (Homewall) | 17 / 984 / 139 | 278 / 470 / 392 | 611 |
| MoonBoard | renders; 2010 and Mini 2025 at low resolution | 16 / 757 / 249 | 4 / 475 / 543 | 587 |
| Tension | photos (Board 1), simple renders (Board 2) | 73 / 783 / 443 | 204 / 394 / 701 | 1,085 |
| Grasshopper | photos | 9 / 312 / 145 | 4 / 192 / 270 | 280 |
| Decoy | photos (layout 2) | 18 / 169 / 267 | 4 / 124 / 328 | 908 |
| So iLL | drawing | – | 0 / 84 / 151 | 340 |

Direction is the weakest field everywhere: from straight in front, which side carries the rim is often a guess.

**Consistency between boards.** Kilter was labelled with rules first and then checked by eye. The other boards were
labelled by eye only. The type shares differ a lot: 35 % jugs on Kilter, 4 % on MoonBoard. Part of that is real,
since the MoonBoard is a crimpy board, but part may come from the method. Comparing boards in the stats needs a
measured accuracy per board, not just for Kilter (see question 3).

## Delivery

As proposed in the [delivery report](2026-11-06-delivery.md): one JSON file per board in the app, labels only. The six
files are 3 to 16 KB compressed each, 65 KB together. No database change.

## Review in test builds

- **Hold-type review** (from build 1 of #69): the Kilter reference set of 153 holds, blind first, then only the
  disagreements.
- **Check hold labels** (new, from build 2): any board with labels, holds on the review list first and the least sure
  of them first. The proposed label is shown, and three buttons record "looks right", "correct it" (type, direction,
  foot only) or "can't tell". The results stay in a file on the phone until they are saved or shared, like the review.

Both are in Settings → About, in test builds only.

## Accuracy

Not measured yet. It follows from the blind round on Kilter. The rule from decision 2 (edge size out of a board's
stats below about 70 % agreement) has nothing to drop yet, because no board has edge sizes.

## The first stats: options to choose from

All of them count hand holds only (start, middle, finish; no foot-only holds), use labels of at least medium
confidence, and say how many holds they rest on. Manual hold tags on a log stay next to the computed labels
(decision 6).

1. **Your hold mix.** The share of each type among the hand holds of your sends, per board and across boards, next to
   the board's average problem: "you send 12 % more slopers than the average Kilter problem".
2. **Strong and weak types.** For each type, your hardest send and your send rate on problems where that type
   dominates (at least 40 % of the hand holds), against your overall level.
3. **Pull direction.** Down-pull, sidepull and undercling shares, the same way.
4. **Year in review card.** "Your year in holds: 41 % edges, 22 % jugs …", for Kilter first if the Kilter labels are
   stable by about 25 November.
5. **Training hint.** The type you climb least, with problems that are heavy in it.

Recommendation: 1 and 2 first, on top of the rebuilt logbook stats; 3 when direction has a measured accuracy.

## Ideas for the send probability (not part of this work)

- Features per problem: hold-type mix, direction mix, the share of small edges, the share of foot-only holds.
- Per climber: send rate by type and direction from the logbook, against the problem's mix.
- Labels carry confidences, so a model can weight them or drop the uncertain ones.

## Open

- The labels of Touchstone, Shiny Wall and most of So iLL need better pictures than the app has.
- Accuracy per board (question 3).
- Three MoonBoard Masters 2019 cells where the hold in the picture does not have the colour of the set the app's
  hold-set map gives it (J2 and E3 listed as Hold Set B, E2 as Original School). This may be a hold-set map error;
  it is worth a separate check.
