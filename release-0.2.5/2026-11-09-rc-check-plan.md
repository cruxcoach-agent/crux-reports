# 0.2.5: what the release candidates are checked for

Plan of 9 November 2026 for the checks of the 0.2.5 release candidates on the test phone. It follows the [release plan](https://github.com/CruxCoach/CruxCoach/milestone/1): RC1 on Mon 16 Nov from the freeze head, stable on 22–24 Nov.

- **RC1 and the last RC** get the full check below.
- **Every RC in between** gets the parts its changes could touch, with what was tested and why.
- Every check is done by hand on the test phone, in the signed build of the release track, and without Google services.
- Results go into the release room, one post per RC (build, commit, what was tested, what works, what is open) and a report here.

## Before RC1 (freeze head, Sun 15 Nov after 18:00 UTC)

1. The database check again on the freeze head: for Board, Secure and Athlete, a fresh install has the same schema as 0.2.4 plus every new migration, the numbering has no gaps, and no old migration was edited.
2. The combined What's New (EN, DE) and `RELEASE_NOTES.md` as one pull request into `feat/0.2.5-release`, from the [first draft](2026-11-09-whats-new-and-release-notes.md), with the lines of PRs that missed the freeze taken out.
3. The What's New dialog rendered in English and German, dark and light, at font size 1.0 and 2.0, 320 dp and 411 dp wide. On release-track builds the dialog cannot appear after an update (their version code is the build number), so the render and its unit test are the check.

## 1. Update with data in it

Install the RC over an earlier build of the release track that has data in it, without uninstalling.

- The app opens without onboarding again, on the board it was on, with its catalogues.
- Logbook, lists, favourites, settings and the account key are all still there and the same.
- Training: workouts, performance values, places, body entries and nutrition days are all still there. A pain value saved on the 0–9 scale reads "x of 10" with the same number.
- Spray walls (if the earlier build had any): walls, versions and problems are still there, and a public wall stays public.
- Restore a 0.2.4 backup into the RC: the logbook comes back, and its body stats show up in training.
- A fresh install of the RC: onboarding, catalogue download and first climb.

## 2. Every 0.2.5 feature, in English and German

| Feature | What is checked |
|---|---|
| Training & nutrition | quick start; Today's suggestion with "Why?"; start a training, log sets, rest and hang timer, end page; swap an exercise; "It hurts" with the 0–10 pain sheet; injury mode; nutrition: find food, barcode scan, typed meal, water; the export contains training data |
| Statistics | logbook overview card; period and board filters; tries until the send; boards compared (logbook with two boards); session recap shared as an image |
| Year in review | open from the statistics with the year picker; tap through every page; share a page: no name, problem names or exact dates unless switched on |
| Shiny Wall | choose a wall and its variant; browse with the filters and categories; light a problem; the map shows Shiny Wall gyms; the account import (#50, with real history entries from #56) |
| Wall games | each of the four games with a board, and on the screen without one |
| Spray walls | new wall from a photo without people; holds suggested (with and without the hold model); set and log a problem; versions; publish, find it at its gym, withdraw; the switch that hides spray walls |
| LED effects | pick an effect in Settings and from a climb's menu; "None" restores the normal colours |
| Community | Settings → Community; "Join on Buzz" opens the browser; the hint after a bug report |
| Bluetooth name | share a board, end sharing: the phone's own name is back |
| If in 0.2.5 | PaintBox (#90), board size check (#55, with #53), hold types on Kilter (#95), contrast (#92) |

Checks with a board use the board simulator; a real board where the feature needs one (PaintBox's gate).

## 3. Around the features

- The main screens still work: board browser, problem page, logbook, lists, board map, settings, backup and restore.
- Dark and light theme, and the largest font size on the screens of the new features.
- No crash during the whole check (the crash buffer is read at the end).

## 4. Before the stable release is published

The release candidates are their own app next to the stable one, so the update from the stable 0.2.4 app to the stable 0.2.5 app is checked with the stable build itself (added on 9 Nov at the maintainer's request):

1. Install the signed stable 0.2.5 over the stable 0.2.4 app on the test phone, without uninstalling, before 0.2.5 is published. The maintainer gives the steps for the signed build.
2. Android accepts it as an update, and the app opens on its own data: logbook, lists, settings and the account key are still there.
3. The databases are updated on the first start (Secure 16 → 18, the new training database), without a crash.
4. The What's New dialog appears once after the update, in the phone's language, and not again after a restart. This is the only build where it can appear after an update; on release-track builds only its render and unit test check it.
5. A quick check of the main screens and the 0.2.5 entry points (training, statistics, Shiny Wall, spray walls).

## Not part of these checks

- Signing and the release workflow: they follow separately.
