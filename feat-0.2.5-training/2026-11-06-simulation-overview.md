# Training simulation: overview (issue #59)

Synthetic athletes run day by day through CruxCoach's real training logic, and automatic checks look at the suggestions over 10 to 16 weeks.
Code and the fixes are in the draft pull request [#62](https://github.com/CruxCoach/CruxCoach/pull/62) (commit 9321b7995), and the athlete model, the checks, their thresholds and the sources are in `docs/en/TRAINING_SIMULATION.md` there.
These reports come from the full run at that commit, after the fixes. Every run is reproducible: each persona has a fixed seed.

## Findings

| # | Persona | Week | What happened | Why it is wrong | Fix or question |
|---|---|---|---|---|---|
| 1 | home-hangboard and 8 others | 1–16 | A legs-and-core day planned 16 leg sets; the weekly maximum is 10 | Filling the chosen time added sets and exercises without looking at the week | Fixed in #62 |
| 2 | youth-15, beginner-board, beginner-home-lb | 1–12 | The block after each climbing day added antagonists: 19 sets a week against a maximum of 11 | The block after climbing ignored the weekly maximum | Fixed in #62 |
| 3 | masters-55, home-hangboard | 1–12 | After that cap, nearly full weeks got sessions with 4 sets in 11 min | A pointless session | Fixed: easy mobility session instead |
| 4 | all 12 | 1–4 | "Finger load rising" appears in weeks 1–4, and later only after a break. Example: home-hangboard asks for finger strength, but its first finger session comes on day 26 | The 28-day normal counts the days before the first entry as rest days, so every new user who climbs regularly looks like a spike for about four weeks | Question 1 |
| 5 | 9 of 12 | all | A full training is suggested on a 6th or 7th day after the week's training days (climbing included) are used up (44 times) | The athlete's number of training days is not respected on Today | Question 2 |
| 6 | home-hangboard, gym-no-board, advanced-taper, always-easy and others | 10–16 | The app's value stays 25–60 % below the athlete's true maximum after 6–14 sessions. Examples: goblet squat 34 kg against 83 kg, max hang 77 kg against 98 kg | Athletes with a lot in reserve train too light for weeks: "3+" is the largest reserve answer, and values rise at most 10 % per set. Part of the gap may be the simulated athlete: its true value is crude for lifts limited by holding the implement | Question 3 |
| 7 | home-hangboard | 3 | Radial/ulnar deviation went from 3 to 5 kg between two sessions | Two weight steps at a small load (+66 %) | Question 4 |
| 8 | beginner-board, rope-outdoor, gym-no-board | 6–12 | A body-weight exercise is planned the same way in five sessions | The summary offers the harder variant; the simulated athlete never takes it | No change: the athlete decides |
| 9 | advanced-taper | all | No separate finger session in ten weeks | Two board days count as finger sessions, and the days around them are recovery days | By design; noted |

Safety checks (all 12 personas, every day): no max finger work during an injury, return ramp, youth or first-year guardrail; none within 48 h of hard climbing (72 h at 55+); no exercise that loads an open injury; no finger work a growing climber should not do; no max finger work on a finger-load spike. Deloads and the taper before the trip date happen.

## Questions for the maintainer

1. **Load normal for new users.** Should the 28-day normal count only from the first logged day?
   - a) Keep it: a careful start for everyone.
   - b) Count from the first logged day once 14 days are logged (**recommended**).
   - c) Skip the careful start when the setup says 3+ years of climbing.
2. **Used-up training days.** What should Today suggest once the week's training days are used up?
   - a) Keep suggesting training.
   - b) Suggest mobility or rest by default, with training still one tap away (**recommended**).
   - c) Only mention it in the reasons.
3. **Values that lag behind.** When every work set of an exercise was "3+", how should the next plan react?
   - a) Keep it: safe but slow.
   - b) Plan the next session two steps higher (**recommended**).
   - c) A larger reserve answer such as "5+". This is a UI change, so it would come later.
4. **Small loads.** Should the planned load rise by at most one weight step per session below about 10 kg?


## Flags at a glance (after the fixes)

| Persona | Weeks | Trainings | Climbing days | Safety | Load | Progress | Plan | Stacking |
|---|---|---|---|---|---|---|---|---|
| Beginner on the board, nothing else | 12 | 17 | 36 | – | – | 2 | 16 | – |
| Intermediate with a hangboard and dumbbells at home | 16 | 64 | 32 | – | 4 | 1 | 1 | – |
| Advanced climber with a trip date | 10 | 39 | 20 | – | 3 | – | 2 | – |
| Rope climber who logs climbing by hand | 12 | 38 | 36 | – | – | 1 | 1 | – |
| Climber aged 55+, in pounds | 12 | 47 | 24 | – | – | – | 8 | – |
| 15-year-old in the gym | 12 | 43 | 36 | – | 1 | – | 11 | – |
| A finger pulley injury | 14 | 52 | 18 | – | 1 | – | 1 | – |
| A week of illness, then three weeks of holiday | 14 | 37 | 20 | – | 2 | – | 3 | – |
| Gym only, no board, then a trip with nothing | 12 | 43 | 36 | – | 1 | 1 | 14 | – |
| Skips half of the planned days | 12 | 29 | 12 | – | – | – | – | – |
| Always says “too easy” | 12 | 49 | 24 | – | 2 | 1 | 12 | – |
| Beginner with dumbbells at home, in pounds | 12 | 43 | 12 | – | – | – | 15 | – |

## Flags by check

- Safety: Max finger work while a return, comeback or injury rule forbids it: none
- Safety: Hard finger session too soon after a hard climbing day: none
- Safety: Exercise that loads an open injury: none
- Safety: Finger work a growing climber should not do: none
- Safety: Max finger sessions too close together for a masters climber: none
- Load: Planned load jumped more than one step or 10 % between sessions: 2 (home-hangboard)
- Load: Max finger work while the finger load is above 1.5 × its normal: none
- Load: The app's value is far from what the athlete can really do: 12 (home-hangboard, advanced-taper, youth-15, pulley-injury, ill-and-away, gym-no-board, always-easy)
- Progress: An exercise stalled for weeks without a change: 6 (beginner-board, home-hangboard, rope-outdoor, gym-no-board, always-easy)
- Progress: No lighter week in a block, or no taper before the date: none
- Plan: Weekly volume of an area far from its target: 40 (advanced-taper, rope-outdoor, masters-55, youth-15, ill-and-away, gym-no-board, always-easy, beginner-home-lb)
- Plan: Suggestion does not fit the session length: none
- Plan: A full training suggested after the week's training days are used up: 44 (beginner-board, home-hangboard, advanced-taper, masters-55, pulley-injury, ill-and-away, gym-no-board, always-easy, beginner-home-lb)
- Plan: Too little variety: none
- Stacking: Reductions stacked into a pointless session: none

## Persona reports

- [beginner-board](2026-11-06-simulation-beginner-board.md) · [day by day](2026-11-06-simulation-beginner-board-days.md)
- [home-hangboard](2026-11-06-simulation-home-hangboard.md) · [day by day](2026-11-06-simulation-home-hangboard-days.md)
- [advanced-taper](2026-11-06-simulation-advanced-taper.md) · [day by day](2026-11-06-simulation-advanced-taper-days.md)
- [rope-outdoor](2026-11-06-simulation-rope-outdoor.md) · [day by day](2026-11-06-simulation-rope-outdoor-days.md)
- [masters-55](2026-11-06-simulation-masters-55.md) · [day by day](2026-11-06-simulation-masters-55-days.md)
- [youth-15](2026-11-06-simulation-youth-15.md) · [day by day](2026-11-06-simulation-youth-15-days.md)
- [pulley-injury](2026-11-06-simulation-pulley-injury.md) · [day by day](2026-11-06-simulation-pulley-injury-days.md)
- [ill-and-away](2026-11-06-simulation-ill-and-away.md) · [day by day](2026-11-06-simulation-ill-and-away-days.md)
- [gym-no-board](2026-11-06-simulation-gym-no-board.md) · [day by day](2026-11-06-simulation-gym-no-board-days.md)
- [skipper](2026-11-06-simulation-skipper.md) · [day by day](2026-11-06-simulation-skipper-days.md)
- [always-easy](2026-11-06-simulation-always-easy.md) · [day by day](2026-11-06-simulation-always-easy-days.md)
- [beginner-home-lb](2026-11-06-simulation-beginner-home-lb.md) · [day by day](2026-11-06-simulation-beginner-home-lb-days.md)
