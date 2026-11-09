# 0.2.5: test plan for the release app

Plan of 9 November 2026, second version: the release-candidate plan of the same morning, turned into one plan from the last merges to the stable release, with an owner for every line. It follows the [release plan](https://github.com/CruxCoach/CruxCoach/milestone/1): every 0.2.5 pull request on `feat/0.2.5-release` by Wed 11 Nov, noon; freeze Sun 15 Nov, 18:00 UTC; RC1 Mon 16 Nov; stable 22–24 Nov.

**Who**
- **Crux:** by adb on the test phone, which runs without Google services. Screenshots of what is checked.
- **Maintainer:** by hand, at a real board or with own data.
- **Crux + simulator:** the maintainer starts the board simulator in the board's mode, Crux drives the app. Crux asks for it with a numbered question and walks other lines meanwhile.

Everything is tested in the release app: the signed builds of the track `feat-0-2-5-release`, announced in this room and in #builds. Each build is installed over the one before it.

## Dates

| When | What | Who |
|---|---|---|
| Tue 10 Nov | Review of #90 (PaintBox) and #95 (hold types) | Maintainer |
| Wed 11 Nov, noon | Every 0.2.5 pull request is on the release branch | Maintainer |
| Wed 11 Nov, afternoon | Migration check on that head; the What's New and release notes PR | Crux |
| Thu 12 Nov | First full walk (sections 1–4) on the first build with everything in it | Crux |
| Thu 12 Nov, evening | Kilter blind round saved: the gate for the Kilter hold-type card | Maintainer |
| Thu 12 – Sun 15 Nov | Every new build walked (section 5); the board checks at a real board (section 6) | Crux, Maintainer |
| Sun 15 Nov, 18:00 UTC | Freeze. Migration check on the freeze head | Crux |
| Mon 16 Nov | RC1: full walk again, installed over the data of the walked builds | Crux |
| Before stable | The signed stable 0.2.5 over the stable 0.2.4 (section 7) | Maintainer, Crux |

## 1. Update with data (Crux)

The release app on the test phone runs build 1000036 (`277534f3e`). Its data comes from two earlier builds: a logbook with sends, a flash and attempts, two lists, a training profile, a private spray wall with two problems, and an injury at pain 9 on the old 0–9 scale. An export was taken before each step.

| Check | Who |
|---|---|
| The first full build installs over it, without uninstalling. The app opens without onboarding, on the board it was on, with its catalogues. | Crux |
| Logbook, lists, favourites, settings and the account key are unchanged; an export after the update matches the one before. | Crux |
| The Secure database goes from 17 to 18 on the first start, without a crash. The spray wall, its version and its two problems are there. | Crux |
| The injury reads "9 of 10"; the comeback plan and its state are kept. Training: workouts, performance values, places, body entries and nutrition days are all there. | Crux |
| A backup made with the stable 0.2.4 restores into the release app: the logbook comes back, and its body stats show up in training. | Maintainer (open question: or Crux with test data) |
| Fresh install, after the update walk: export, uninstall, install the current build. Onboarding, catalogue download, first climb; the logbook opens while the catalogue is still being finished (#115); restore the export. Then a spray wall and an injury again, so the next update runs over data too. | Crux |

## 2. Every 0.2.5 feature (Crux, German and English)

The full walk runs in German; then every screen of each feature again in English. Findings go to the room in the last column.

| Feature | What is walked | Who | Findings to |
|---|---|---|---|
| Training and nutrition | Quick start; Today's suggestion with "Why?"; start a training, log sets, rest and hang timer, end page; swap an exercise; numbers with their units (#99); "It hurts" with the 0–10 pain sheet; injury mode, the comeback plan and its weekly look-back (#98, #114 and their follow-ups); the weekly plan counts planned climbing (#98); nutrition: find food, barcode scan, typed meal, water; the export contains training data | Crux | #feat-0.2.5-training |
| Statistics | The logbook overview before the statistics (#86); period and board filters; tries until the send; boards compared (two boards in the logbook); session recap shared as an image | Crux | #feat-0.2.5-analytics |
| Year in review | Open it from the statistics with the year picker; tap through every page; share a page with name, problem names and dates off and on; the dark status bars once merged | Crux | #feat-0.2.5-year-in-review |
| Shiny Wall | Choose a wall and its variant; browse with filters and categories; the map shows Shiny Wall gyms; the legal notes (#54); the account import: preview, logbook with flashes, attempts and projects, favourites and lists, a second import adds no duplicates, disconnecting removes the sign-in | Crux | #feat-0.2.5-shiny-wall |
| | Light a problem | Crux + simulator | |
| Wall games | Each of the four games on the screen without a board (#101's layout) | Crux | #feat-0.2.5-shiny-wall |
| | Each game with a board | Crux + simulator | |
| Spray walls | A new wall from a photo without people; holds suggested, with and without the hold model; set and log a problem; versions; publish, find it at its gym, withdraw; a climb is deleted only once a relay took it back, and kept with a message when offline (#104); a wall refresh (#107); the switch (#106): off hides spray walls on the map and in the year in review, and the entry stays only while something of your own may still be out | Crux | #feat-0.2.5-spray-walls |
| LED effects | Pick an effect in Settings and from a climb's menu; "None" brings back the normal colours | Crux | #feat-0.2.5-done-led-effects |
| | The effects on the wall | Crux + simulator | |
| Community | Settings → Community; "Join on Buzz" opens the browser; the hint after a bug report | Crux | #feat-0.2.5-community |
| Board size check (#55) | The picker row for Kilter (not for MoonBoard, Quantum, Shiny Wall); the sheet without a connection, markers on the holds for several sizes; "Wrong holds on the board?" in a Kilter climb's menu | Crux | #dev |
| | Lit dots, "Light again", "No" → another size, "Yes" saves the size | Crux + simulator | |
| PaintBox (#90) | Without a board: paint, save, load, a photo, board switch, the largest font | Crux | #feat-0.2.5-paintbox |
| | The simulator list in #90: Kilter API 2 and 3, MoonBoard, Quantum (a climb replaces the picture), the playlist guard, a picture of another board | Crux + simulator | |
| Hold types (#95) | Every card locked before the round; Settings → About: the hold-type review and "Check hold labels"; after the round, only the Kilter card opens | Crux | #feat-hold-types |
| Relay traffic (#109) | Every feature that talks to the relays, as listed in #109: developer messages, announcements, community climbs live sync, profiles, backup and restore, the Lightning invoice (not paid), spray walls, reconnect after airplane mode | Crux | #dev |
| Bluetooth name | Share a board, end the sharing: the phone's own name is back | Crux + simulator | #dev |

## 3. Around the features (Crux)

- The main screens still work: board browser, problem page, logbook, lists, board map, settings, backup and restore.
- Contrast (#92): every new screen in the light and the dark theme.
- The largest font size on the screens of the new features.
- No feature needs Google services: barcode scan, map and the Shiny Wall sign-in work on the test phone.
- No crash during the whole walk: the crash log is read at the end.

## 4. Smoke check (Crux, every build)

The build installs over the one before it; the app opens; board browser, a problem, the logbook, training Today, the statistics and Settings open; the crash log is empty.

## 5. Build by build, from Thu 12 Nov (Crux)

- The first build with every pull request gets the full walk (sections 1–4).
- Every later build gets the smoke check plus everything its new commits could touch, read from the commits since the last walked build. Shared code (relays, Bluetooth, databases, navigation, theme) widens the walk to every feature that uses it.
- Findings go to the feature room of the change: build, commit, steps, what happens, a screenshot. A crash, data loss or a privacy problem is posted at once, in the feature room and here.
- One short line per build here: build, commit, what was walked and why, findings with links.

## 6. Only the maintainer (by hand)

| What | When |
|---|---|
| The Kilter blind round in the hold-type review; the Kilter card opens only after it | Saved by Thu 12 Nov, evening |
| PaintBox on a Kilter wall: the wall steps in #90, API 2 or 3 first | Before Sat 14 Nov, in the release app |
| The LED effect "Restart" on a Kilter board | At the same wall session |
| The board size check at a real board: the lit dots sit on the holds of the board's size | At the same wall session |
| The board simulator for the "Crux + simulator" lines | When Crux asks |
| A backup from the stable 0.2.4 restored into the release app (section 1) | Any build from Thu 12 Nov |

## 7. Release candidates and the stable build

- **Before RC1 (freeze head, Sun 15 Nov after 18:00 UTC), Crux:** for Board, Secure and Athlete, a fresh install has the same schema as 0.2.4 plus every new migration, the numbering has no gaps, and no old migration was edited. The What's New dialog rendered in English and German, dark and light, at font size 1.0 and 2.0, 320 dp and 411 dp wide. On release-app builds the dialog cannot appear after an update (their version code is the build number), so the render and its unit test are the check.
- **RC1 and the last RC, Crux:** the full walk (sections 1–4), installed over the data of the builds walked before.
- **Every RC in between, Crux:** section 5.
- **Before the stable release is published, Maintainer and Crux:** the release candidates are their own app next to the stable one, so the update from the stable 0.2.4 to the stable 0.2.5 is checked with the stable build itself (added on 9 Nov at the maintainer's request):
  1. Install the signed stable 0.2.5 over the stable 0.2.4 app on the test phone, without uninstalling, before 0.2.5 is published. The maintainer gives the steps for the signed build.
  2. Android accepts it as an update, and the app opens on its own data: logbook, lists, settings and the account key are still there.
  3. The databases are updated on the first start (Secure 16 → 18, the new training database), without a crash.
  4. The What's New dialog appears once after the update, in the phone's language, and not again after a restart.
  5. A quick check of the main screens and the 0.2.5 entry points (training, statistics, Shiny Wall, spray walls).

## Not part of this plan

- Signing and the release workflow ([#110](https://github.com/CruxCoach/CruxCoach/pull/110)): they follow separately.

## Changes from the first version (9 Nov, morning)

- Testing starts before the freeze, in the release app, build by build, with an owner for every line.
- The update with data runs on the first build with every pull request (Thu 12 Nov) instead of RC1: by then the migrations are final, and RC1 installs over the data of the walked builds.
- New lines for #86, #92, #98, #99, #104, #106, #107, #109, #114 and #115, merged on 9 Nov, and the maintainer's checks at a real board.
