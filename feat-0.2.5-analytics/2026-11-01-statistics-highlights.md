# Logbook statistics, reorganised (2026-11-01)

Room: #feat-0.2.5-analytics · issue [#44](https://github.com/CruxCoach/CruxCoach/issues/44) · draft pull request [#48](https://github.com/CruxCoach/CruxCoach/pull/48)

**Third version.** The first version of this report showed the new elements the maintainer chose from the [ideas](2026-11-01-stats-ideas.md): at a glance, milestones, how your boards feel, tries until the send and the session recap. The maintainer then asked to fit them into the existing statistics so that nothing is shown twice. This version shows the result: one overview at the top of the logbook, and statistics where every number and chart appears once.

The renders come from the design test with a made-up logbook on three boards, on a German phone, dark and light. The phone section shows the same build on the test phone.

## What was shown twice

| Before | Now |
|---|---|
| Six tiles at the logbook top and "at a glance" at the top of the statistics | One overview card at the logbook top |
| Grade pyramid, outcomes by grade, flash-or-later donut, sent climbs per grade | One chart: problems per grade (flash, sent later, not yet sent) |
| Rolling level and hardest new send per month | One progress chart, one line per board |
| Activity calendar, log entries over time, weekly volume | One activity card: calendar or entries per week |
| Board chips and the tappable comparison table | Board chips, each with its sends |
| Records row and period comparison | The overview card and the milestones |

## The logbook top

![Logbook top, dark](2026-11-01-glance-top.png)

- One card instead of six tiles: the hardest send and hardest flash, the last 30 days against the 30 days before, and the milestones as small chips (weeks in a row, new grades, 50/100/250… sends, biggest day).
- It always covers the whole logbook and every board. Tapping it opens the statistics; the ⓘ explains the numbers.
- The period chips of the list moved into the logbook filter, next to result, board and angle. The list and the statistics no longer share a period.
- Each day in the list has a recap button next to its date.

## The statistics, top to bottom

![Statistics, upper half, dark](2026-11-01-sheet-top.png)
![Statistics, lower half, dark](2026-11-01-sheet-bottom.png)

1. **Filters:** the period, then the board chips (only with more than one board). Each board chip shows its sends in the period, so the chips are the comparison of how much you climb where.
2. **The period in four numbers:** sends, tries, climbing days, problems.
3. **How your boards feel** (only with enough data): one sentence and a dot per board on a scale of grades.
4. **Progress:** the rolling performance level, one line per board when you look at all boards together, each line ending in its current grade.
5. **Problems per grade:** each problem once, by its best result: flashed, sent later, or not sent yet. Tap a grade for its numbers.
6. **Tries:** until the send (flash, 2, 3, 4–5, 6+ per board), per grade (one bar per board), per month (one line per board).
7. **Activity:** the calendar, or entries per week by grade band on a time axis, so weeks off show as gaps.

![Entries per week, dark](2026-11-01-weekly.png)

8. **Angles** and **holds**, as before.

## One colour language

- Light blue means a flash, darker blue more tries, grey a problem not yet sent: in problems per grade and in tries until the send.
- Each board has one colour in every chart and on every dot.
- Grade colours (green, orange, red, purple) mark grades and grade bands: the record tiles, the recap and entries per week.
- Orange stays the app's accent: chips, the calendar, the angles.

## How your boards feel

How the estimate works:
- For each problem, the tries until its first send, counted across sessions.
- For a pair of boards, a line through the logarithm of the tries over the grade, with one slope for both boards. The slope says how many more tries a harder grade costs you, and the gap between the boards how many more tries the same grade costs on the other board. The gap divided by the slope is how much harder the other board is, in grades of your grade scale near your usual grade.
- It only shows when it says something: at least 8 sent problems on each board, sends at two or more of the same grades, tries that clearly rise with the grade, and an uncertainty of at most one grade. The pale band around a dot shows that uncertainty.
- In the made-up logbook, MoonBoard was set 1.6 difficulty steps harder and Tension 0.6 easier. The estimate shows about 1½ grades harder and about half a grade easier.

## Session recap

![Session recap, dark](2026-11-01-session-recap.png)

- Opens from the recap button next to a date in the logbook. The summary at the end of a timed session now shows the same card, with its time and intensity details below it.
- The card shows the date, the boards, sends, flashes, tries, the hardest grade, the sends per grade and the milestones of that day. "Share as image" shares exactly this card through the phone's share menu.

## Light theme

![Logbook top, light](2026-11-01-glance-top-light.png)
![Statistics, upper half, light](2026-11-01-sheet-top-light.png)

## On the test phone

Test build 5 (commit 7d153ec9) on the test phone, with the small made-up logbook of the earlier phone test: three boards, 21 entries.

![Logbook top and statistics on the phone](2026-11-01-phone-build5-1.png)
![Grades, tries, recap and share on the phone](2026-11-01-phone-build5-2.png)

- The overview card reads well. Tapping it opens the statistics.
- The board chips show their sends: "Alle 21", "Kilter 11", "Tension 8", "MoonBoard 2".
- How your boards feel stays hidden here, because MoonBoard has only 2 sent problems. That is intended.
- With only two problems, MoonBoard's bar in "tries until the send" is hollow, as the legend says.
- "Share as image" opens the phone's share menu with the card as its preview.
- Fixed after this check, in the next build: the overview appeared a moment after the list and pushed it down in one jump (it now grows in); the period chips in the logbook filter were orange unlike the other filter chips; the activity calendar started with empty months before the first entry.
- Not checked on the phone: the end-of-session summary with the card (only in the renders), and the light theme (only in the renders).

## The other ideas

None of these is built. Each could go into a place that already exists, so no new card is needed:

1. **Open projects:** a filter in the logbook ("Open projects": tried, not yet sent, newest try first, with tries so far).
2. **Project grade per board:** a faint band in "Tries per grade" across the grades where you usually need 3 to 6 tries.
3. **Median:** next to the average in the details when you tap a grade.
4. **One grade over the months:** tapping a grade in "Tries per grade" shows that grade month by month.
5. **Angles:** a small angle switch in the tries card (all angles / 40° / 50°).
6. **Points per week:** needs a points table first and would be a new card, so later.

## Tests

- At a glance, milestones and the recap (11 tests), the board feel and the tries buckets (5), stats across boards (9), the statistics computation (46), the statistics sheet with its info and activity selector (1), board colours (3): all pass locally. CI runs the full suite.
- The removed charts took their tests with them. The tests on flash detection now check the grades chart instead of the donut.
- The design test renders all pictures above; CI skips it.
