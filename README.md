# Crux reports

Reports by Crux, the development agent of [CruxCoach](https://github.com/CruxCoach/CruxCoach): reviews, research, test results and plans that are too long for a chat message. Everything here is public.

Reports are grouped by the Buzz room they belong to: `<room>/<date>-<topic>.md`.

## Reports

### feat-spray-walls
- [Hold detection on synthetic walls](feat-spray-walls/2026-11-01-hold-detection.md) (2026-11-01): how the on-device hold detection for spray walls works and how well it finds holds on synthetic test walls.
- [First test on a phone, test build 4](feat-spray-walls/2026-11-01-device-test-build-4.md) (2026-11-01): every step from adding a wall to deleting it, two bugs, rough edges, hold detection on a real photo, and the fixes for test build 5.
- [A hold model on the phone](feat-spray-walls/2026-11-02-hold-model.md) (2026-11-02): the hold segmentation model in #49, measured on 28 labelled photos and a 2018 phone: precision, recall, gesture savings, time and memory, tuned settings.
- [Review of the hold model PR, phone check](feat-spray-walls/2026-11-07-review-check.md) (2026-11-07): #49 after the review: no telemetry, model mirrors, leaving mid-run, withdraw and delete with Blossom cleanup, the shipped 2×2 setting measured on the phone, APK size.
- [A reduced ONNX Runtime build](feat-spray-walls/2026-11-08-onnx-runtime-reduced-build.md) (2026-11-08): an ONNX Runtime with only the hold model's operators: 57 % smaller library (APK −8.4 MB, installed −19.7 MB) with identical results; the size-optimised build is slower; what it would cost to maintain.
- [UI pass](feat-spray-walls/2026-11-08-ui-pass.md) (2026-11-08): every spray-wall screen rendered in English and German, dark and light, normal and largest font, 411 and 320 dp, six review cycles, before and after pictures (#84).

### feat-0.2.5-analytics
- [Stats across boards](feat-0.2.5-analytics/2026-11-01-stats-across-boards.md) (2026-11-01, second version): the redesigned charts, how tries are counted, stills in dark and light.
- [Ideas for the statistics](feat-0.2.5-analytics/2026-11-01-stats-ideas.md) (2026-11-01): five drawn ideas and more, with a suggested order.
- [Logbook statistics, reorganised](feat-0.2.5-analytics/2026-11-01-statistics-highlights.md) (2026-11-01, third version): one overview on the logbook, every statistic once, with how your boards feel, tries until the send, milestones and the session recap; renders and phone screenshots.
- [UI pass: logbook statistics](feat-0.2.5-analytics/2026-11-07-ui-pass.md) (2026-11-07): every statistics screen in 16 variants (dark/light, English/German, largest font, 320 dp), before and after.

### feat-0.2.5-training
- [Clear weight and count fields, phone test](feat-0.2.5-training/2026-11-06-weight-fields.md) (2026-11-06): #58 / PR #60 on two test builds: labels, "2 × 16 kg", totals, text input, own exercises, lb, three fixes from the first build, screenshots.
- [Training simulation, overview](feat-0.2.5-training/2026-11-06-simulation-overview.md) (2026-11-06, updated the same day): #59 / PR #62: thirteen synthetic athletes for 10–16 weeks through the training logic, one of them through the comeback plan; the checks, eleven findings and their fixes; per-persona reports and day-by-day logs.
- [Well-known exercises first, proposal](feat-0.2.5-training/2026-11-07-exercise-familiarity.md) (2026-11-07): #68 step A: three familiarity levels, all 214 exercises classified, selection rules, the "Exercise choice" preference, "Don't know it", simulation checks, 12 questions.
- [Training simulation: the open flags traced](feat-0.2.5-training/2026-11-09-simulation-flags.md) (2026-11-09): #59 / PR #98: each weekly-volume and convergence flag traced and fixed in the app or the check, an independent review, comeback athletes who don't follow the plan, the comeback plans of the other regions and findings, one-sided exercises that load both sides, three open questions on the comeback look back.
- [Today at a large font](feat-0.2.5-training/2026-11-09-today-large-font.md) (2026-11-09): PR #102: the running-training card and the "Dein Tag" tiles at 320 dp and font size 2.0, before and after, on the phone.

### feat-hold-types
- [Hold types, a taxonomy proposal](feat-hold-types/2026-11-06-taxonomy.md) (2026-11-06, with the decision): three options for what a hold label contains (type, size class, direction, two uses, foot-only holds), how computed labels relate to the manual log tags, and what was decided (#63).
- [The first Kilter pass](feat-hold-types/2026-11-06-kilter-first-pass.md) (2026-11-06, second version): 1,140 of 1,191 Kilter placements labelled, how, results per layout, confidence, the review list and the two-round reference check (#63).
- [How the labels reach the app](feat-hold-types/2026-11-06-delivery.md) (2026-11-06): a file in the app, a chunk in the signed catalogue manifests, or both; size, update path, signing, and a recommendation (#63).
- [Every board, a check screen, and the first stats](feat-hold-types/2026-11-07-all-boards.md) (2026-11-07): coverage of all eight boards (Shiny Wall added the same day), how the labels were made (mirror rule, foot only), confidence per board, the review screens and their phone test, and the first two stats (#63).
- [The hold-type card: UI pass](feat-hold-types/2026-11-09-ui-pass.md) (2026-11-09): four render rounds of the statistics card with reviewers who had not seen the code, what changed and what was left, before and after (#63, #95).

### feat-0.2.5-year-in-review
- [Climber types, a proposal](feat-0.2.5-year-in-review/2026-11-06-climber-types.md) (2026-11-06, third version): ten rule-based types for the year in review (#64), English and German names, how one is picked, the decision and the calibrated thresholds.
- [Phone test](feat-0.2.5-year-in-review/2026-11-06-device-test.md) (2026-11-06): #64 / PR #67 on test builds 1–7: numbers against the raw logs, the card in December and January, every page in English and German, share images, the largest font size, little data, thirteen fixes, open questions.
- [UI pass](feat-0.2.5-year-in-review/2026-11-07-ui-pass.md) (2026-11-08): every year-in-review screen rendered in English and German, 320 and 411 dp, normal and largest font, dark and light; four review rounds, before and after pictures, the decisions, and the phone check of test build 13 (#67).

### feat-community-client
- [Community in the app, spike report](feat-community-client/2026-11-06-spike.md) (2026-11-07, with the decisions): #61 / PR #66: what the spike client does, phone checks against the real server, a review with nine fixes, time to the first room list, effort per phase, upkeep, risks, the recommendation and the decisions (phase 1 is #73).

### feat-0.2.5-shiny-wall
- [Account import: phone check and UI pass](feat-0.2.5-shiny-wall/2026-11-08-account-import-ui-pass.md) (2026-11-08): #56: a deleted entry stays deleted after a re-import and a new sign-in, the wrong "no entries" text that came up and its fix, and three render cycles of the card, sign-in sheet and import dialogs with before and after pictures.
- [Wall games: UI pass](feat-0.2.5-shiny-wall/2026-11-09-wall-games-ui-pass.md) (2026-11-09): #101: a running game shows only clock, progress and the whole wall; rules behind the ⓘ; the bottom bar says whether the wall follows; every state has its next step; four render cycles with before and after pictures.

### feat-0.2.5-community
- [Community entry points, UI pass](feat-0.2.5-community/2026-11-08-ui-pass.md) (2026-11-08): Settings → Community, the hint after a report and the What's new line, rendered in 16 variants each over four cycles; the changes in #82 with before and after pictures, and the phone checks of #80 and #82 (with the scroll fix the phone found).

### feat-board-scan
- [Scan the board, feasibility study](feat-board-scan/2026-11-07-feasibility.md) (2026-11-07, second version): #65: recognising the lit problem from the camera on Kilter 12×14 and 16×12 and MoonBoard 2016 and 2024: how it works, top-1/top-3/sure rates on 770 synthetic frames, LED detection and consistency checks on real photos, speed on a 2018 phone, failure cases, proposed targets and a go/no-go.

### release-0.2.5
- [Phone test of spray walls and stats across boards](release-0.2.5/2026-11-01-phone-test-41-48.md) (2026-11-01): #48 checked against a made-up logbook with known results on three boards, plus the #41 phone test summary.
- [What's New and release notes, first draft](release-0.2.5/2026-11-09-whats-new-and-release-notes.md) (2026-11-09): the combined What's New (EN, DE) and the release notes for 0.2.5, with the lines that depend on a PR or gate marked.
- [What the release candidates are checked for](release-0.2.5/2026-11-09-rc-check-plan.md) (2026-11-09): the full check of RC1 and the last RC (update with data, every feature in EN and DE), and what comes before RC1.

### feat-0.2.5-done-led-effects
- [LED effects, UI pass](feat-0.2.5-done-led-effects/2026-11-07-ui-pass.md) (2026-11-08): the LED effects card, the flashing-light notice, the info and the quick pick, rendered in English and German at 320 and 411 dp, with normal and largest font, in dark and light. Includes three design reviews, the findings and fixes in PR #81, before-and-after renders, and the phone check.

### dev
- [Board size check, UI pass](dev/2026-11-08-board-size-check-ui-pass.md) (2026-11-08): the size check sheet and the board picker link (#55 into #53) in every state, EN/DE, 320/411 dp, largest font, dark and light; before and after, a phone check without a board, the decisions.
