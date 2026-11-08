# 0.2.5: What's New and release notes, first draft

Draft of 9 November 2026, written against the release branch at `277534f3e` and the open pull requests of the [0.2.5 plan](https://github.com/CruxCoach/CruxCoach/milestone/1). The final version follows from the freeze head (Sun 15 Nov) as one pull request into `feat/0.2.5-release`.

Lines marked **[if …]** depend on a pull request or a gate; they drop out (or shrink) if it misses the freeze. The release-key part is left out for now and comes later.

## 1. What's New (the dialog after the update)

Seven short lines and an "Also" line. Order: what most people will use first. About 540 characters in English (0.2.3: 340 in six lines, 0.2.4: 350 in four), since 0.2.5 is the biggest release so far. Places are named only where a feature is hard to find (Community, PaintBox); the rest sits in the main menu, the board picker or the statistics.

### English

**New in 0.2.5**

- • Training & nutrition – today's training from your logbook, 200+ exercises and food targets.
- • Statistics – an overview first, tries until the send, your boards compared, session recaps.
- • Year in review – your climbing year as pages to share, from 1 December.
- • Shiny Wall – choose it in the board picker and light its problems**[if #50:**, or import your logbook**]**.
- • Spray walls – photograph your own wall, and the phone finds the holds. **[if spray walls stay in 0.2.5]**
- • Wall games – Floor is lava, Endurance, Hold thief and Traverse.
- • Community on Buzz – talk to the developers and test new builds first (Settings → Community).

*Also: LED effects for Kilter, a board size check **[if #53]**, PaintBox (Settings → Extras) **[if #90]** and your Bluetooth name back after sharing.*

### Deutsch

**Neu in 0.2.5**

- • Training & Ernährung – das Training für heute aus deinem Logbuch, über 200 Übungen und Ernährungsziele.
- • Statistiken – erst die Übersicht, Versuche bis zur Begehung, deine Boards im Vergleich, Session-Rückblicke.
- • Jahresrückblick – dein Kletterjahr als Seiten zum Teilen, ab 1. Dezember.
- • Shiny Wall – in der Board-Auswahl wählen und ihre Probleme leuchten lassen**[if #50:**, oder dein Logbuch übernehmen**]**.
- • Spraywände – fotografiere deine eigene Wand, und das Handy findet die Griffe. **[if spray walls stay]**
- • Wand-Spiele – Der Boden ist Lava, Ausdauer, Griffdieb und Quergang.
- • Community auf Buzz – sprich mit den Entwicklern und teste neue Versionen zuerst (Einstellungen → Community).

*Außerdem: LED-Effekte für Kilter, eine Prüfung der Board-Größe **[if #53]**, PaintBox (Einstellungen → Extras) **[if #90]** und dein Bluetooth-Name kommt nach dem Teilen zurück.*

### Notes on the wording

- The names are the ones on the screens: "Training & nutrition" / "Training & Ernährung" in the main menu, "Session recap" / "Session-Rückblick", "Versuche bis zur Begehung", "Spray walls" / "Spraywände", the four game names, "Extras", "Community".
- The community line is the one already on the branch (#51, #82), unchanged. The Shiny Wall and wall-game lines of #54 are folded into the lines above, so on its rebase #54 can leave `whatsnew_025_body` as the branch has it. That removes one of its two conflicts.
- If the hold-type card from #69 passes its gate, it goes into the "Also" line: "hold types in the Kilter statistics" / "Grifftypen in den Kilter-Statistiken".
- If the dialog reads too long on a small phone, the first candidates for the "Also" line are wall games and community.

### What the final pull request changes (from the freeze head)

- `whatsnew_025_body` (EN, DE): the seven lines, with `&#160;` before each dash like the community line.
- a new `whatsnew_025_hint` (EN, DE) and its `Text` in `Release025WhatsNewDialog`, styled like the 0.2.4 hint.
- `CommunityJoinTest`: the community line check matches a substring, since the body has more lines.
- `RELEASE_NOTES.md`: the text in section 2.
- Not in it: registering `RELEASE_025`, `versionCode` 11, `versionName` and the release date. They belong to the release preparation.

## 2. Release notes (`RELEASE_NOTES.md`, GitHub release and Zapstore)

> # CruxCoach 0.2.5 — 2026-11-2x
>
> This release adds training and nutrition for climbers, statistics that compare your boards, a year in review, Shiny Wall with wall games, and spray walls.
>
> ## Highlights
> - **Training and nutrition, built for climbers.** A new area in the main menu
>   suggests today's training from your board logbook, your week, your
>   equipment and how you feel, and says why. Over 200 exercises in English and
>   German with steps and pictograms, a training logger that plans loads from
>   your own values, rest and hang timers, places with their equipment, and a
>   coach that learns from what you change. Nutrition sets protein,
>   carbohydrate and energy targets that follow your training days; foods come
>   from offline food tables, a barcode scan or an optional photo model that
>   runs on the phone. An injury mode spares what hurts, and a comeback plan
>   helps you build up again together with your doctor or physio. Training data
>   stays on the phone and is part of the encrypted backup; injuries only when
>   you switch them on.
> - **Statistics that compare your boards.** The logbook opens with an
>   overview: your hardest send and flash, the last 30 days against the 30
>   before, and your milestones. The statistics show every number once, how
>   many tries you need until the send, and, if you climb on more than one
>   board, how the boards compare and how they feel for you. Each logbook day
>   and each timed session has a recap to share as an image.
> - **Your year in review.** Your climbing year across all your boards,
>   imported logbooks included, as pages to tap through: volume, hardest sends,
>   rhythm, highlights and your climber type. Every page can be shared as an
>   image, without your name, problem names or exact dates unless you switch
>   them on. A card invites you from 1 December to 31 January, and the
>   statistics keep it all year. It is computed on the phone; nothing is
>   uploaded.
> - **Shiny Wall and wall games.** Choose your Shiny Wall Standard wall in the
>   board picker, browse its problems with its own categories and light them
>   over Bluetooth; gyms with a Shiny Wall appear on the board map.
>   **[if #50:** Import your Shiny Wall logbook, favourites and lists, read-only,
>   under Settings → Board accounts & imports.**]** Wall games (Floor is lava,
>   Endurance, Hold thief and Traverse) turn the board into a game on Shiny
>   Wall, Kilter, the other Aurora boards and MoonBoard.
> - **Spray walls. [if spray walls stay in 0.2.5]** Photograph your own wall,
>   and the phone suggests the holds; an optional hold model (33 MB, offline
>   once downloaded) finds holds of every colour with their real shape. Set
>   problems with start, hand, foot and finish holds and log them in a private
>   logbook. A wall stays on your phone unless you make it public; then others
>   find it at its gym on the board map.
>
> ## Other improvements
> - **LED effects** for Kilter boards, contributed by Dapeebb (#21): the lit
>   climb can pulse, flash or run through a rainbow (Settings → Board &
>   Bluetooth → LED effects).
> - **PaintBox [if #90]**, contributed by Hugie (#77): paint pictures on your
>   board's LEDs, every hold a pixel, sent once or live (Settings → Extras).
> - **Board size check [if #53]:** if other holds light up than the app shows,
>   the board picker and a climb's ⋯ menu light a few marked holds so you can
>   compare and pick the size that fits. The board picker also shows how common
>   each board size is in gyms.
> - **Hold types [if the Kilter card passes its gate]:** the Kilter statistics
>   show which kinds of hand holds your problems use and where your send rate
>   is higher or lower than usual.
> - **Community:** Settings → Community explains the CruxCoach community on
>   Buzz, where you can talk to the developers and test new builds first.
> - After sharing a board with other apps, your phone gets its own Bluetooth
>   name back on every path, also after a crash or a restart, and connecting
>   to a car ends sharing.
> - Catalogue updates no longer wait 15 seconds per board when a relay never
>   answers, and a catalogue import frees its temporary file at once.
> - The Kilter Homewall 10x12 image shows its real holds.
> - Links in Settings → About and the MoonBoard data request no longer close the
>   app on a phone without a browser or an email app.
> - **[if #92]** Orange and status colours are readable in the light and the
>   dark theme.
>
> ## Compatibility
> CruxCoach 0.2.5 requires **Android 9 or newer**, like 0.2.4, and works without
> Google services. A 0.2.4 backup restores in 0.2.5, and 0.2.4 restores a
> 0.2.5 backup without the training data.

### Notes on the release notes

- Training, statistics, spray walls and the year in review are new for everyone coming from 0.2.4, so the fixes made to them during 0.2.5 (weight fields, the coach's weekly limits, pain scale 0–10, the UI passes) are part of the features, not listed as fixes.
- Contributors are credited the way `CHANGELOG.md` does: Dapeebb for the LED effects, Hugie for PaintBox.
- `CHANGELOG.md` keeps the full detail; nothing here contradicts it.
- The backup sentence rests on the backup tests on the branch; the upgrade check of RC1 (a 0.2.4 build with data in it) checks it again.
