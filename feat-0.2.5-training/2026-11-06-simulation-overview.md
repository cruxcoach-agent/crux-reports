# Training simulation: overview (issue #59)

Synthetic athletes run day by day through CruxCoach's real training logic, and automatic checks look at the suggestions over 10 to 16 weeks. One of them follows the comeback plan after a finger injury.
Code and the fixes are in the draft pull request [#62](https://github.com/CruxCoach/CruxCoach/pull/62) (commit 707ecde58). The athlete model, the checks with their thresholds, and the sources are in `docs/en/TRAINING_SIMULATION.md` there.
These reports come from the full run at that commit. Every run is reproducible because each persona has a fixed seed.

## Findings

| # | Persona | Week | What happened | Why it is wrong | Status |
|---|---|---|---|---|---|
| 1 | home-hangboard and 8 others | 1–16 | A legs-and-core day planned 16 leg sets; the weekly maximum is 10 | Filling the chosen time added sets and exercises without looking at the week | Fixed |
| 2 | youth-15, beginner-board, beginner-home-lb | 1–12 | The block after each climbing day added antagonists: 19 sets a week against a maximum of 11 | The block after climbing ignored the weekly maximum | Fixed |
| 3 | masters-55, home-hangboard | 1–12 | After that cap, nearly full weeks got sessions with 4 sets in 11 min | A pointless session | Fixed: easy mobility session instead |
| 4 | all 12 | 1–4 | "Finger load rising" in weeks 1–4 | The 28-day normal counted the days before the first entry as rest | Fixed (maintainer's answer 1) |
| 5 | 9 of 12 | all | A full training on a 6th or 7th day after the week's training days were used up (44 times) | The number of training days was not respected | Fixed (answer 2) |
| 6 | home-hangboard, gym-no-board, advanced-taper, always-easy and others | 10–16 | The app's value stayed 25–60 % below the truth | "3+" is the largest answer, and values rise at most 10 % per set | Fixed (answer 3); 5 cases left |
| 7 | home-hangboard | 3 | Radial/ulnar deviation 3 → 5 kg between two sessions | Two steps at a small load | Fixed (answer 4) |
| 8 | beginner-board, rope-outdoor, gym-no-board | 6–12 | A body-weight exercise planned the same way in five sessions | The athlete never takes the harder variant offered | No change: the athlete decides |
| 9 | advanced-taper | all | No separate finger session in ten weeks | Two board days count as finger sessions | By design |
| 10 | pulley-comeback | 2–5 | The athlete's Saturday training became "your training days are done" | The new rule from answer 2 counted the plan's short daily sessions (3 to 8 minutes) as training days | Fixed: comeback sessions do not use up a day |
| 11 | pulley-comeback | 3–8 | Each strength session started from the load of the morning's light 30-second tendon holds; the half-crimp holds reached 22 kg at the last stage instead of the stage's 33 kg | The comeback plan took the last load of the same exercise from any of its sessions | Fixed: each kind of session keeps its own loads |

## The maintainer's answers, as implemented

1. The 28-day load normal counts from the first logged day once 14 days are logged. Until then the careful start stays (no max finger work).
2. Once the week's training days (climbing included) are used up, Today suggests mobility or rest, with training one tap away.
3. After a session in which every work set was "3+", the next one plans at least two steps more. This applies to strength exercises only, not to finger work, and not during an injury, the return ramp, a comeback session or the youth and first-year rules.
4. Below 10 kg a load rises at most one step per session. This wins over 3.

## The comeback plan

The persona `pulley-comeback` gets a pulley strain of the right hand in week 2. They start the plan at stage 0 with a doctor's finding and their own reference values, and follow it through the same calls as the comeback screen and Today's card: the diary, the plan's prompts, every session Today lists as due (set by set), and each session's highest pain. The injured finger has a simulated truth of its own: a tolerance that heals over about seven weeks, pain in each set from load against that tolerance, and irritation that fades. The athlete is careful and honest and accepts every proposal. The week-by-week table is in [its report](2026-11-06-simulation-pulley-comeback.md).

Result: the plan went from stage 0 to stage 5, one stage a week. The athlete ended it in week 8, six weeks after the injury. Session pain stayed at 3 or below, and the half-crimp holds of the injured hand rose from 5 kg to the last stage's 33 kg. None of the comeback checks flagged anything: loads stayed within the stage's range or effort, the next stage came only after a week within the pain rule, sessions were spaced as the stage plans, there was no board session before the stage allows hard climbing, and no stage got stuck while it stayed calm.

Not simulated yet: comeback plans for other regions, a plan started later than the injury, an athlete who does not follow the plan, the board logbook from the app's own board, and swaps or "another suggestion" on the card other than "too easy".

## Flags at a glance

| Persona | Weeks | Trainings | Climbing days | Safety | Load | Progress | Plan | Stacking |
|---|---|---|---|---|---|---|---|---|
| Beginner on the board, nothing else | 12 | 17 | 36 | – | – | 2 | – | – |
| Intermediate with a hangboard and dumbbells at home | 16 | 64 | 32 | – | – | 1 | – | – |
| Advanced climber with a trip date | 10 | 39 | 20 | – | – | – | 1 | – |
| Rope climber who logs climbing by hand | 12 | 38 | 36 | – | – | – | – | – |
| Climber aged 55+, in pounds | 12 | 47 | 24 | – | – | – | 4 | – |
| 15-year-old in the gym | 12 | 43 | 36 | – | 1 | – | 11 | – |
| A finger pulley injury | 14 | 52 | 18 | – | 1 | – | – | – |
| A finger pulley injury with the comeback plan | 14 | 55 | 24 | – | – | – | – | – |
| A week of illness, then three weeks of holiday | 14 | 35 | 20 | – | – | – | 2 | – |
| Gym only, no board, then a trip with nothing | 12 | 48 | 36 | – | 1 | – | 1 | – |
| Skips half of the planned days | 12 | 31 | 12 | – | – | – | – | – |
| Always says “too easy” | 12 | 50 | 24 | – | 2 | – | 5 | – |
| Beginner with dumbbells at home, in pounds | 12 | 42 | 12 | – | – | – | 10 | – |

## Flags by check

- Safety: Max finger work while a return, comeback or injury rule forbids it: none
- Safety: Hard finger session too soon after a hard climbing day: none
- Safety: Exercise that loads an open injury: none
- Safety: Finger work a growing climber should not do: none
- Safety: Max finger sessions too close together for a masters climber: none
- Safety: Comeback load above its stage: none
- Safety: Next comeback stage offered while it still hurt: none
- Safety: Comeback sessions closer than their stage allows: none
- Safety: Board session suggested while the comeback stage holds it back: none
- Load: Planned load jumped more than one step or 10 % between sessions: none
- Load: Max finger work while the finger load is above 1.5 × its normal: none
- Load: The app's value is far from what the athlete can really do: 5 (youth-15, pulley-injury, gym-no-board, always-easy)
- Progress: An exercise stalled for weeks without a change: 3 (beginner-board, home-hangboard)
- Progress: No lighter week in a block, or no taper before the date: none
- Progress: Comeback plan stuck on a stage although it stayed calm: none
- Plan: Weekly volume of an area far from its target: 34 (advanced-taper, masters-55, youth-15, ill-and-away, gym-no-board, always-easy, beginner-home-lb)
- Plan: Suggestion does not fit the session length: none
- Plan: A full training suggested after the week's training days are used up: none
- Plan: Recovery suggested although training days are left: none
- Plan: Too little variety: none
- Stacking: Reductions stacked into a pointless session: none

What is left: 5 values far from the truth, 3 stalls (body-weight work, finding 8), and 34 weeks in which an area's volume is below half its goal or above 1.25 × its maximum. From a first look, the weeks above a maximum include the credit for climbing that is logged later in the week. The weeks below a goal are mostly areas the persona leaves out: finger work for the beginner without a hangboard, legs for the 15-year-old, push for the always-easy athlete. They have not been traced one by one yet.
