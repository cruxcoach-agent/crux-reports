# Year in review: climber types, a proposal (#64)

*2026-11-06, third version: with the maintainer's decision and the calibrated thresholds.*

## Decision (2026-11-06)

1. The ten types stay. Explorer and Repeat Lover are kept in reserve, in case calibration shows a type that almost
   nobody or almost everybody gets.
2. Picking: B, the strongest match. If there is time before the test build, one small "also" type is added (C with
   one, not two).
3. German names: a, the neutral nouns as listed.
4. Comeback Kid: only "after a break", on the card and in the image, never an injury.

The thresholds are calibrated on synthetic logbooks so that no type, All-Rounder included, takes more than about a
quarter of them. Once the type card is in a test build, the room is asked which type people get, as the real-world
check.

## Calibration (2026-11-06, third version)

400 made-up logbooks over two years, drawn from wide ranges: how often and how regularly people climb (with busy
weeks, an off-season and breaks), on one to four boards, at which angles, how hard, how stubbornly they project,
how often they repeat, whether they train off the wall. All 400 reach the full review. The test that checks
the thresholds is part of the code (`ClimberTypeCalibrationTest`), so a later change cannot quietly tip the balance.

Three rules had to change shape, because their score grew with sheer volume and one type took everyone:

- **Projector:** "5 problems after 10+ tries" became a share: at least 8 % of the new problems took 10 tries or
  more. A busy climber reached five such problems by spring, so 63 % of the logbooks were Projectors.
- **Board Hopper:** scored by the share of the third board, so three boards used evenly count more than three
  boards where one barely shows.
- **Comeback Kid:** a fixed score once the rule is met. Scoring by the length of the break let every long summer
  break outweigh all other types.

The thresholds now, and how many of the logbooks get each type:

| Type | Rule (all within the year) | Share |
|---|---|---|
| Flash Machine | at least 70 % of the new problems flashed (at least 20) | 7 % |
| Projector | at least 8 % of the new problems took 10+ tries, or 3.5 tries on average (at least 15) | 13 % |
| Mileage Monster | 14 sends per board day on average (at least 20 days) | 7 % |
| Steep Specialist | at least 75 % of the entries at 45° or steeper (MoonBoard: 40°) | 11 % |
| Board Hopper | a third board with at least 10 % of the entries | 14 % |
| Clockwork | climbing in 85 % of the weeks, or a run of 16 weeks | 14 % |
| Rising Star | +2 grades on the main board over last year, or first to last three months | 8 % |
| Strength Lab | 20 workouts, on at least 45 % of the training days | 13 % |
| Comeback Kid | a finished comeback plan, or 8+ climbing days after a break of 8 weeks | 4 % |
| All-Rounder | nothing else fits | 5 % |

76 % of the logbooks also fit a second type, shown small as "also". Explorer and Repeat Lover stay in reserve. The
numbers rest on made-up logbooks only; the real check is asking the room which type people get once it is in a
test build.

---

*The proposal as it was put to the decision:*

The year in review ([#64](https://github.com/CruxCoach/CruxCoach/issues/64)) ends with "your climber type": a
fun, rule-based type, so that everyone above the minimum amount of data gets one, with the rule shown on the card.
This is the proposal: ten types, how one is picked, and the open choices.

## What the rules can use

Everything comes from data that is already on the phone; nothing new is stored.

- **Board logbook**, all boards including imported logbooks: every entry with board, angle, tries, send or not,
  grade on the shared difficulty scale, and day.
- **First send of a problem**: the first send of a (board, problem, angle) in the year, with all tries up to it,
  counted as in the statistics of [#44](https://github.com/CruxCoach/CruxCoach/issues/44). A **flash** is a first
  send on the first try with no earlier entry on that problem.
- **Climbing days**: days with a board entry or a climbing day logged by hand (gym, rock, another board).
- **Training**: off-board workouts and the comeback plan.

Not used: the time of day (imported entries often have only a date), anything about other users, and the reason
for a break.

## The ten types

Thresholds are starting values. They will be checked on synthetic logbooks of very different climbers, so that
every type actually occurs and no type takes almost everyone. Every type needs the year's minimum amount of data;
below it, the review shows a short "your year so far" and no type.

| # | English | German | One line (EN / DE) | Rule (all within the year) |
|---|---|---|---|---|
| 1 | Flash Machine | Flash-Maschine | Sees it, sends it. / Anschauen, durchsteigen. | At least 40 % of the first sends were flashes, with at least 20 first sends. |
| 2 | Projector | Projekt-Profi | Never lets a problem go. / Lässt kein Projekt los. | At least 5 problems first sent after 10 or more tries, or on average 4 or more tries per first send (at least 15 first sends). |
| 3 | Mileage Monster | Meter-Monster | More problems, more fun. / Mehr Boulder, mehr Spaß. | On average 10 or more sends per board day, over at least 20 board days. |
| 4 | Steep Specialist | Überhang-Fan | The steeper, the better. / Je steiler, desto lieber. | At least 60 % of the board entries at 45° or steeper (on a MoonBoard: 40°), with at least 50 entries. |
| 5 | Board Hopper | Board-Hopper | At home on every board. / Zu Hause an jeder Wand. | At least 3 boards with 10 % or more of the entries each. |
| 6 | Clockwork | Uhrwerk | Week in, week out. / Woche für Woche. | A climbing day in at least 75 % of the weeks since the first one of the year (at least 12 weeks), or a run of 16 weeks or more. |
| 7 | Rising Star | Rakete | Up the grades. / Steil nach oben. | On the main board, the hardest first send is at least 2 grades above last year's. Without last year: the level of the last three months is at least 2 grades above the first three. |
| 8 | Strength Lab | Kraftpaket | Builds the engine off the wall. / Holt sich die Kraft abseits der Wand. | At least 20 workouts, and workouts on at least 30 % of all training days (workout days and climbing days). |
| 9 | Comeback Kid | Comeback-Talent | Came back and kept climbing. / Zurückgekommen und drangeblieben. | A comeback plan finished, or a break of 6 weeks or more followed by at least 8 climbing days. The card and the image say "after a break", never why. |
| 10 | All-Rounder | Allround-Talent | A bit of everything. That's a style too. / Von allem etwas. Auch das ist ein Stil. | When no other type fits. Its card names the user's strongest number instead of a rule. |

Grades are never merged across boards: "Rising Star" compares the main board with itself (the board with the most
entries), on the same grade scale the statistics show.

### Alternatives that could replace one of the ten

- **Explorer / Entdeckungs-Typ:** at least 90 % of the sends on problems not sent before, and at least 150
  problems.
- **Repeat Lover / Lieblingsboulder-Fan:** at least 30 % of the sends are repeats of problems already sent.
- **Night Owl / Nachteule** and **Early Bird / Frühaufsteher:** most climbing after 20:00 or before 9:00. Not
  recommended: imported entries often have no time of day, so the type would rest on part of the data.

## How one type is picked

- **A, first match:** the rules are checked in a fixed order and the first that applies wins. Simple, but the
  order decides, and the first types take most people.
- **B, strongest match (recommended):** every rule gives a score, the user's value divided by its threshold
  (for example 62 % flashes ÷ 40 % = 1.55). The highest score of at least 1 wins; ties go by the table order.
  Without any score of at least 1: All-Rounder. The card shows the winning rule with the user's number, for
  example "62 % of your first sends were flashes. Flash Machines start at 40 %."
- **C, B with traits:** as B, plus up to two more types that also apply, shown small under the main type ("also:
  Clockwork, Board Hopper"). More to share, a little more text to fit.

## German names

- **a, neutral nouns (recommended):** Flash-Maschine, Uhrwerk, Kraftpaket, Comeback-Talent, Allround-Talent, as in
  the table. They read the same for everyone.
- **b, gender-inclusive forms:** e.g. "Projektierer:in", "Senkrechtstarter:in".
- **c, classic idioms:** e.g. "Dickkopf", "Senkrechtstarter", "Stehaufmännchen". Lively, but grammatically
  masculine.

## Questions

1. Are these ten the right set, or should one of the alternatives replace a type (which)?
2. How should one type be picked: A, B (recommended) or C?
3. German names: a (recommended), b or c? Any names you would change?
4. The comeback type: is "after a break", never naming an injury, right, also in the shared image?
