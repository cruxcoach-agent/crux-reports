# Scan the board: feasibility study (Kilter and MoonBoard)

Issue [#65](https://github.com/CruxCoach/CruxCoach/issues/65) · 2026-11-07 · first version

Can a phone tell which problem is lit on a board from the camera alone, offline, whatever app lit it? This study
measures how often it names the right problem, how often it is confidently wrong, how often it is unsure, and how
long it takes, on Kilter (12×14 and 16×12) and MoonBoard (2016 and 2024). No UI was built for it; everything ran
as plain Kotlin on a server and, for the timing, on a 2018 mid-range phone.

## Short answer

**Go, with one condition.** On synthetic frames the recogniser names the right problem first in 94 % of free-view
scans on Kilter 12×14 and MoonBoard 2016 (85–87 % on Kilter 16×12 and MoonBoard 2024), has it among the first three
in 89–98 %, and was **never sure and wrong in 770 frames** (450 with problems as people climb them, 280 with any
problem, 40 mirrored). On a 2018 mid-range phone it answers in about 0.9 s per frame for popular Kilter problems
and 0.4 s for MoonBoard 2016. The condition: real photos are clearly harder than the renders. On the only
public set of real photos, the detector finds two in three hand LEDs, against nearly all in the renders, so the first
step after a go should be a test build checked on a real board, before the rest of the UI.

- **A climber in front** (a quarter to a third of the lit holds hidden): top-1 drops to 45–73 %, and the recogniser
  says "not sure" much more often. It still offers its best three, and it was never sure and wrong.
- **"Sure" is strict on purpose:** in free view 67 % of Kilter 12×14 scans and 39 % of MoonBoard 2016 scans are sure
  on a single frame. Otherwise the app shows the best three to pick from, or keeps looking at the next frames.
- **Speed:** searching the whole Kilter catalogue (213,000 problems) takes seconds on an older phone, so the 20,000
  most climbed problems (95 % of all logged ascents) are searched first. MoonBoard problems are read straight off
  the board.
- **Mirrored Kilter problems** are found too, at the cost of a second search when the first is not sure.

## Results

Each frame is one look at a lit board. **Top-1**: the right problem comes first. **Top-3**: it is among the first
three. **Sure**: the recogniser would name the problem on its own; otherwise the app would offer the best three to
pick from. **Wrong while sure**: frames where it was sure and wrong, the number that matters most.

"Free view" frames show every lit hold; in "climber" frames a person-shaped silhouette hides some of them (on
average a quarter to a third of the problem's lit holds).

### Problems as people climb them

Problems drawn in proportion to their logged ascents.

| Board | View | Frames | Top-1 | Top-3 | Sure | Wrong while sure |
|---|---|--:|--:|--:|--:|--:|
| Kilter 12×14 | free view | 83 | 94 % | 98 % | 67 % | 0 |
|  | climber | 67 | 73 % | 85 % | 43 % | 0 |
|  | all | 150 | **85 %** | **92 %** | **57 %** | **0** |
| Kilter 16×12 | free view | 53 | 85 % | 89 % | 68 % | 0 |
|  | climber | 47 | 49 % | 62 % | 17 % | 0 |
|  | all | 100 | **68 %** | **76 %** | **44 %** | **0** |
| MoonBoard 2016 | free view | 62 | 94 % | 97 % | 39 % | 0 |
|  | climber | 38 | 53 % | 71 % | 0 % | 0 |
|  | all | 100 | **78 %** | **87 %** | **24 %** | **0** |
| MoonBoard 2024 | free view | 47 | 87 % | 89 % | 28 % | 0 |
|  | climber | 53 | 45 % | 58 % | 0 % | 0 |
|  | all | 100 | **65 %** | **73 %** | **13 %** | **0** |

### Any problem

Problems drawn uniformly from the whole catalogue, including ones nobody has climbed.

| Board | View | Frames | Top-1 | Top-3 | Sure | Wrong while sure |
|---|---|--:|--:|--:|--:|--:|
| Kilter 12×14 | free view | 54 | 98 % | 100 % | 76 % | 0 |
|  | climber | 46 | 70 % | 78 % | 41 % | 0 |
|  | all | 100 | **85 %** | **90 %** | **60 %** | **0** |
| Kilter 16×12 | free view | 28 | 93 % | 93 % | 46 % | 0 |
|  | climber | 32 | 41 % | 53 % | 22 % | 0 |
|  | all | 60 | **65 %** | **72 %** | **33 %** | **0** |
| MoonBoard 2016 | free view | 36 | 97 % | 97 % | 67 % | 0 |
|  | climber | 24 | 58 % | 71 % | 0 % | 0 |
|  | all | 60 | **82 %** | **87 %** | **40 %** | **0** |
| MoonBoard 2024 | free view | 33 | 85 % | 91 % | 15 % | 0 |
|  | climber | 27 | 70 % | 78 % | 0 % | 0 |
|  | all | 60 | **78 %** | **85 %** | **8 %** | **0** |

### Mirrored problems (Kilter)

The first 40 Kilter 12×14 frames, mirrored, so that each shows the mirrored problem. With the mirror search the
right problem (marked as mirrored) comes first in 80 % of them and is in the top three in 90 %; sure in 50 %, never
sure and wrong. The same 40 frames unmirrored: 88 %, 93 % and 53 %. Leaving the mirror search on for ordinary,
unmirrored frames costs some top-1 (85 % → 81 % on the 150 Kilter 12×14 frames: when neither pass is sure, a
mirrored candidate sometimes comes first) and causes no confident wrong answer.

### Speed on a 2018 mid-range phone

The same Kotlin code, run from the command line on the phone (eight Cortex-A53 cores), on 720×1280 frames:

| Step | Median | Slowest |
|---|--:|--:|
| Finding the lit LEDs (every frame) | 0.15–0.2 s | 0.3 s |
| Kilter 12×14, the 20,000 most climbed problems | 0.8 s | 0.9 s |
| Kilter 12×14, the whole catalogue (213,000 problems), when the first part is not sure | 2.6 s | 6.6 s |
| MoonBoard 2016, read off the board | 0.17 s | 1.0 s |
| MoonBoard 2024, read off the board | 0.5 s | 0.6 s |
| MoonBoard 2024, catalogue search when the board cannot be located | 2.4 s | |

Kilter: 20 frames, MoonBoard: 10 frames per set, eight threads; the answers were the same as on the server. The
catalogue search scales with the number of problems, which is why the popular part goes first. A Kilter catalogue
takes about 50 MB of memory in this first version; that can be cut to about half.

## How it works

Everything runs on the phone in plain Kotlin, without Google services, OpenCV or a neural network. Frames are never
stored or uploaded.

1. **Find the lit LEDs.** A pixel counts as LED light when it is clearly more colourful than its surroundings (a lit
   rim or LED dot on a grey or dark board), not just colourful (painted walls, mats, coloured holds). Neighbouring
   pixels form blobs; a blob that sits inside a colourful area, or that is far too large, is dropped, and the arcs
   of one lit rim are merged.
2. **Give each LED a role from its colour.** Start, hand, finish and foot have fixed colours per lighting app. The
   recogniser knows Kilter's standard scheme, CruxCoach's default scheme and the MoonBoard's, and fits a small hue
   shift per frame for the camera's white balance. Kilter's green start and cyan hand colours record only about 40°
   apart in photos, so they are first treated as one colour and separated later by their hue order.
3. **Undo the camera's tilt.** The phone's gravity sensor gives the camera's tilt and roll, and the board angle comes
   from the board settings. Only the camera's sideways angle to the board is unknown; the recogniser tries a few.
   After that, the board looks as if photographed straight on, up to scale and position.
4. **Kilter: match against the catalogue.** For every problem of the selected board, its highest and lowest holds
   are paired with the highest and lowest lit LEDs of the same colour. Each pairing places the board; a loose pass
   collects the problem's other holds and a tight pass counts the holds that sit on a lit LED of the right colour.
   Popular problems are searched first: the 20,000 most climbed problems hold about 95 % of all logged ascents on
   both Kilter sizes, so the rest of the catalogue is only searched when the popular part gives no sure answer.
   The best 100 candidates are then fitted more precisely and scored: matched holds count for a problem, holds that
   should be lit but are not, LEDs on the board that it does not explain, and colour contradictions count against
   it. Problems with identical holds count as one; the more climbed one is shown first.
5. **MoonBoard: read the board directly.** MoonBoard holes sit on a regular grid, so a problem matched one column
   or row off can look just as good as the right one. Instead, the recogniser first finds the board itself: the lit
   LEDs and the board's own coloured holds (yellow on the 2016 set, blue on the 2024 set) all sit on the grid, which
   gives its spacing and phase, and the pattern of coloured holds says which column and row is which. Then the lit
   holes are read off and looked up in the catalogue directly, without a search. Coloured holds that should be visible
   but are not also show where a climber stands, so a dark hold there does not count against a problem. On the
   2024 set, blue holds and blue LEDs share a colour; once the board is located, a blob on a blue hold only counts
   as lit when it is clearly brighter than the paint.
6. **Mirrored problems (Kilter).** A mirror image of the frame shows a mirrored problem as the original one, so the
   same search runs once more on the mirrored LEDs when the first pass is not sure.

Missing holds are expected (a climber in front, dim foot LEDs), so a missing hold costs less than an unexplained
LED, and a missing foot costs least.

### When an answer is "sure"

- **Kilter:** the best problem's evidence is strong (score ≥ 5), it leads the next one by at least 2.5, at least
  60 % of its holds and at least 7 holds are matched (or every hold of a smaller problem), at most 3 lit LEDs on the
  board stay unexplained, and the matched LEDs sit close to their holds (on average within 0.3 hole spacings).
- **MoonBoard:** the board was located, every hold of the problem is lit and seen, every lit hole belongs to it, and
  no other problem fits as well. If the board cannot be located, the recogniser still offers its best three but is
  never sure.

These thresholds are deliberately strict: a "not sure" costs one tap (pick from three), a confident wrong answer
costs trust. In the app, a problem would also have to be the sure answer on a few consecutive frames.

## Test data

- **Synthetic frames.** The board geometry and layout images that ship with the app, with one catalogue problem lit
  in the scheme of a lighting app, seen by a pinhole camera from a random spot: 1.8–5.5 m from the board, up to 1 m to
  the side, 1.0–1.9 m high, rolled up to 5°, board angles 20–55° (Kilter) or 25/40° (MoonBoard), focal length ±15 %.
  Half the frames have a climber-shaped silhouette in front of the lower part of the problem (some in a shirt of an
  LED colour); up to three stray coloured lights sit around the board; blur, motion blur, noise, exposure, white
  balance and JPEG compression vary. The sensor readings given to the recogniser carry noise (gravity ±1°, board
  angle ±2°, focal length ±5 %). Frames are 720×1280, the size the camera delivers for analysis. They contain the
  manufacturers' layout images, so none are shown here.
- **Real photos.** The only public set of lit-board photos found: 20 phone photos and screenshots of lit Kilter
  boards from [eastonlee/kilterboard](https://huggingface.co/datasets/eastonlee/kilterboard) (originally Roboflow
  "kilter/kilter" v8, CC BY 4.0), with lit holds labelled by colour. They have no sensor data and no problem names,
  so they test the LED detection. Several show climbers, so no image from them appears here.

## Real photos: the weak spot

The synthetic frames are kinder than real photos. On the 20 real photos, the detector finds:

| LED colour (Kilter scheme) | Found |
|---|--:|
| purple (finish) | 21 of 24 (88 %) |
| green (start) | 30 of 37 (81 %) |
| blue/cyan (hand) | 92 of 142 (65 %) |
| orange (foot), recorded as yellow | 16 of 123 (13 %) |

and 71 of its 244 blobs are not on a labelled lit hold (reflections, coloured holds, screens). The photos have no
sensor data, are partly screenshots and crops, and show no problem names, so they cannot give a top-1 rate; in a
first run with the prototype, only one of them got a clean answer (every lit hold explained). Feet barely matter for the answer (they
weigh least), but a hand LED found only two times in three does, and real photos also add glare and reflections the
renders do not have.

This is the largest open risk. It needs real frames from a real board, with the phone's sensors, which only a test
build can deliver.

## Failure cases

- **A climber in front.** With a quarter to a third of the lit holds hidden, many problems share what is still
  visible. The recogniser then says "not sure" far more often and offers three; it was never sure and wrong in
  these frames. On the MoonBoard, reading the board directly, with its coloured holds showing where the climber
  stands, raised top-1 with a climber from about 26 % to about 50 %.
- **Lit rims around big holds** (Kilter) sit up to half a hole spacing off the hole or split into two arcs. Fixed by
  fitting the pose under the camera's known tilt (an affine map after rectification instead of a free perspective
  map) and by not counting the second arc as an extra LED. Before that fix, a small problem matched in a corner of
  the board could be "sure" while ignoring the rest of the lit problem.
- **Kilter 16×12 is weaker than 12×14** (top-1 about 15 points lower overall). In these renders, about one lit LED in ten on
  that layout is hidden behind a big hold and never detected (one in fifty on 12×14).
- **Blue holds on the MoonBoard 2024 set** have the colour of the blue hand LEDs. Before the board is located they
  look alike; after, a blob on a blue hold only counts when it is clearly brighter than the paint. When the board
  cannot be located (too few blue holds visible, heavy occlusion), the 2024 set falls back to the catalogue search
  and is never sure.
- **Rarely climbed problems** on Kilter: the popular part of the catalogue is searched first, so a problem outside
  the 20,000 most climbed is found only by the slower full search.

## What the app would need

- CameraX analysis frames at 1280×720 (CameraX is already used by the barcode scanner), the gravity sensor, the
  focal length from the camera characteristics, and the board angle from the board settings.
- A compact index of the selected board's catalogue (hole positions, holds and roles per problem, popularity),
  built once from the local catalogue: about 10 MB as a file for each Kilter size (213,000 and 222,000 problems),
  3.0 MB for MoonBoard 2016 (98,000) and 1.5 MB for MoonBoard 2024 (44,000). While scanning, a Kilter index takes
  about 50 MB of memory in this first version.
- For MoonBoard sets, the positions and colours of the board's own coloured holds, taken once from the board image
  that ships with the app.
- Several frames per scan: a problem counts once it is the sure answer on consecutive frames; a follow mode keeps
  scanning and switches when the lit set changes.

## Proposed targets

For the maintainer to set; this is my proposal for when the feature is good enough to ship as experimental:

1. **Trust:** at most 1 confident wrong answer in 100 scans on a real board.
2. **Usefulness:** the right problem in the top 3 for at least 9 of 10 scans with the whole problem in view.
3. **Speed:** a sure answer within 1.5 s on a 2018 phone for popular problems; full-catalogue answers may take
   longer while the camera stays on the board.

On synthetic frames, all three hold for Kilter 12×14 and MoonBoard 2016; Kilter 16×12 and MoonBoard 2024 just miss
the second one (89 % with problems as people climb them). None of them is shown on real frames yet.

## Next steps

1. The maintainer's go or no-go, and the targets.
2. With a go: a test build with the scan entry and camera view from #65, so the LED detection and the numbers can be
   checked on a real board, then the result card, the "not sure" and "not in the catalogue" states and the follow
   mode.
3. Tension and the other boards after Kilter and MoonBoard.
4. Photos of lit boards from the community (no people in them) to tune the detection on real light.
