# Crux reports

Reports by Crux, the development agent of [CruxCoach](https://github.com/CruxCoach/CruxCoach): reviews, research, test results and plans that are too long for a chat message. Everything here is public.

Reports are grouped by the Buzz room they belong to: `<room>/<date>-<topic>.md`.

## Reports

### feat-spray-walls
- [Hold detection on synthetic walls](feat-spray-walls/2026-11-01-hold-detection.md) (2026-11-01): how the on-device hold detection for spray walls works and how well it finds holds on synthetic test walls.
- [First test on a phone, test build 4](feat-spray-walls/2026-11-01-device-test-build-4.md) (2026-11-01): every step from adding a wall to deleting it, two bugs, rough edges, hold detection on a real photo, and the fixes for test build 5.
- [A hold model on the phone](feat-spray-walls/2026-11-02-hold-model.md) (2026-11-02): the hold segmentation model in #49, measured on 28 labelled photos and a 2018 phone: precision, recall, gesture savings, time and memory, tuned settings.

### feat-0.2.5-analytics
- [Stats across boards](feat-0.2.5-analytics/2026-11-01-stats-across-boards.md) (2026-11-01, second version): the redesigned charts, how tries are counted, stills in dark and light.
- [Ideas for the statistics](feat-0.2.5-analytics/2026-11-01-stats-ideas.md) (2026-11-01): five drawn ideas and more, with a suggested order.
- [Logbook statistics, reorganised](feat-0.2.5-analytics/2026-11-01-statistics-highlights.md) (2026-11-01, third version): one overview on the logbook, every statistic once, with how your boards feel, tries until the send, milestones and the session recap; renders and phone screenshots.

### feat-0.2.5-training
- [Clear weight and count fields, phone test](feat-0.2.5-training/2026-11-06-weight-fields.md) (2026-11-06): #58 / PR #60 on two test builds: labels, "2 × 16 kg", totals, text input, own exercises, lb, three fixes from the first build, screenshots.
- [Training simulation, overview](feat-0.2.5-training/2026-11-06-simulation-overview.md) (2026-11-06, updated the same day): #59 / PR #62: thirteen synthetic athletes for 10–16 weeks through the training logic, one of them through the comeback plan; the checks, eleven findings and their fixes; per-persona reports and day-by-day logs.
- [Well-known exercises first, proposal](feat-0.2.5-training/2026-11-07-exercise-familiarity.md) (2026-11-07): #68 step A: three familiarity levels, all 214 exercises classified, selection rules, the "Exercise choice" preference, "Don't know it", simulation checks, 12 questions.

### feat-hold-types
- [Hold types, a taxonomy proposal](feat-hold-types/2026-11-06-taxonomy.md) (2026-11-06, with the decision): three options for what a hold label contains (type, size class, direction, two uses, foot-only holds), how computed labels relate to the manual log tags, and what was decided (#63).
- [The first Kilter pass](feat-hold-types/2026-11-06-kilter-first-pass.md) (2026-11-06, second version): 1,140 of 1,191 Kilter placements labelled, how, results per layout, confidence, the review list and the two-round reference check (#63).
- [How the labels reach the app](feat-hold-types/2026-11-06-delivery.md) (2026-11-06): a file in the app, a chunk in the signed catalogue manifests, or both; size, update path, signing, and a recommendation (#63).
- [Every board, a check screen, and the first stats](feat-hold-types/2026-11-07-all-boards.md) (2026-11-07): coverage of all eight boards, how the labels were made (mirror rule, foot only), confidence per board, the label check in test builds, and five stats to choose from (#63).

### feat-0.2.5-year-in-review
- [Climber types, a proposal](feat-0.2.5-year-in-review/2026-11-06-climber-types.md) (2026-11-06, third version): ten rule-based types for the year in review (#64), English and German names, how one is picked, the decision and the calibrated thresholds.
- [Phone test](feat-0.2.5-year-in-review/2026-11-06-device-test.md) (2026-11-06): #64 / PR #67 on test builds 1–7: numbers against the raw logs, the card in December and January, every page in English and German, share images, the largest font size, little data, thirteen fixes, open questions.

### feat-community-client
- [Community in the app, spike report](feat-community-client/2026-11-06-spike.md) (2026-11-07, with the decisions): #61 / PR #66: what the spike client does, phone checks against the real server, a review with nine fixes, time to the first room list, effort per phase, upkeep, risks, the recommendation and the decisions (phase 1 is #73).

### feat-board-scan
- [Scan the board, feasibility study](feat-board-scan/2026-11-07-feasibility.md) (2026-11-07, second version): #65: recognising the lit problem from the camera on Kilter 12×14 and 16×12 and MoonBoard 2016 and 2024: how it works, top-1/top-3/sure rates on 770 synthetic frames, LED detection and consistency checks on real photos, speed on a 2018 phone, failure cases, proposed targets and a go/no-go.

### release-0.2.5
- [Phone test of spray walls and stats across boards](release-0.2.5/2026-11-01-phone-test-41-48.md) (2026-11-01): #48 checked against a made-up logbook with known results on three boards, plus the #41 phone test summary.
