# PeriMove acceptance cases

> **What this is.** The acceptance cases that accompany the recommendation rules: rule cases (inputs and expected result) and screen and flow checks. Test counts in this repository are **as reported by Lovable** for the final build (324 passing tests and a clean build); they show that the specified behaviors passed, not that the product helps anyone. Rules are described in [recommendation-rules.md](recommendation-rules.md).
>
> **How the case count grew.** The rules specification had **32 acceptance cases** when the acceptance plan was written (October 13, before the build). The numbered set grew to **62** over the build, all by October 15 and all before submission, as the design changed:
> - Cases 33 to 37: added in the review of the second build prompt (gentle-session timing and the switch lines).
> - Cases 38 to 46, 50 to 52 and 53 to 54: added for the 15-minute standing session and its versions.
> - Flow checks 47 to 49: added with the changes to Today's setup and the greyed times on the check-in.
> - Cases 55 to 58: added when greying was extended to the gentle and open-to-suggestion choices (October 15, night).
> - Cases 59 to 62: added with the "no easier version" soreness line (October 15, night).
> - Cases 7, 8, 12, 27 and 28 kept their numbers but were revised when the standing session made no-equipment strength possible.
>
> The 62 cases are the specification's acceptance set. They are not the same as the automated tests: the final build's test suite (324 tests reported by Lovable) is larger and numbers its tests separately. Earlier documents that say "32 cases" describe the specification before this growth.

## Build gates
- **P0:** the core loop completes for every session; unsupported combinations show a mismatch screen, never a workout; the prototype label and Stop are always visible; no answers leave the browser.
- **P1:** explanations are accurate, overrides and stopped-early work, tips follow their rules.
- **P2:** closing-screen reminder file, tips list screen, Simpler instructions chip.

## Screen and flow checks

These were written before the final build. The build changed afterward (journey stages, a redesigned recommendation page, no name field), so treat them as the original screen-level checks, not a record of each check being re-run. Gates: P0 core, P1 important, P2 cut first.

| ID | Screen | Check | Gate |
|---|---|---|---|
| A1 | Onboarding | Setup options are floor space, standing space, stable chair (to sit on) and stable table or counter (to lean on); no standing-only option | P0 |
| A2 | Onboarding | Answers save on this device and survive a reload; Reset my information clears them and returns to onboarding | P0 |
| A3 | Check-in | Movement type before time; strength shows 20 and 30, gentle shows 10, open to suggestion shows all | P0 |
| A4 | Check-in | Today's setup prefilled; Edit opens the same choices; changes apply to this visit only | P0 |
| A5 | Check-in | Choosing gentle hides Soreness and More breaks; open to suggestion shows them | P1 |
| A6 | Check-in | Every optional control can be skipped and a recommendation is still produced | P0 |
| A7 | Recommendation | Match, effort or lighter, soreness, single-version and override lines follow the templates and use only what the user entered | P0 |
| A8 | Recommendation | Each exercise shows its selected version; a non-suggested choice shows "you chose" and the override line | P0 |
| A9 | Recommendation | Dead bug shows "One version for now" and has no switch | P0 |
| A10 | Recommendation | Other options list only eligible sessions, at most two, each with its reason | P0 |
| A11 | Recommendation | A gentle session offered for 20 or 30 minutes shows the shorter-than-time line with the displayed estimate | P1 |
| A12 | Recommendation | G10's two standing exercises show only if standing space is selected; turning them off changes the estimate to about 8 min | P1 |
| A13 | Recommendation | More breaks keeps S20 eligible at 20 minutes and shows the longer estimate with a neutral note | P1 |
| A14 | Mismatch | Unmet needs come from the user's inputs; M4 wins when nothing is eligible | P0 |
| A15 | Mismatch | Edit my check-in and Edit today's setup are one tap from every mismatch screen | P0 |
| A16 | Guided, strength | Set complete starts rest; Add 30 s, Skip rest and Pause/Resume work; the last set leads to the next exercise | P0 |
| A17 | Guided, strength | Switching version mid-exercise applies to the remaining sets only | P1 |
| A18 | Guided | Skip exercise moves on with no penalty wording; Stop asks to confirm and then leads to reflection | P0 |
| A19 | Guided, gentle | Timed blocks advance on their own; Next moves on early; no sets, rests or version switch | P0 |
| A20 | Guided | The prototype label and Stop are visible on every session screen | P0 |
| A21 | Reflection | Finished: effort, fit and adjust-over-weeks questions; "What didn't work?" only for Partly or Not well | P0 |
| A22 | Reflection | Stopped early: "Thanks for trying this" and where the user stopped; skipped if nothing completed | P1 |
| A23 | Reflection | Easier or harder tip only if an exercise done has that variant; gentle never gets one; gentle harder shows skip-or-fewer-repeats | P1 |
| A24 | Tips | Hidden tips never render; visible tips show source, review date and "General information, not personal advice" | P1 |
| A25 | Closing | Done leads to the closing screen; Start another check-in clears answers and keeps the saved setup | P0 |
| A26 | Closing | Add a reminder downloads a calendar file in the browser; nothing is sent | P2 |
| A27 | Privacy | No request carries check-in or reflection answers; only onboarding fields are in local storage | P0 |
| A28 | Content | Every exercise shows written cues even when its demonstration is a placeholder | P1 |

## Rule acceptance cases
**Test defaults.** Where a case does not state an input, use: type strength; 20 minutes; equipment dumbbells; setup floor space, standing space, stable chair and stable table or counter; energy medium; rest somewhat; effort moderate; soreness none; More breaks off; Simpler instructions off. A setup named in a case replaces the default setup ("X only" means exactly X); "no X" removes X and keeps the rest. Case 25 uses open to suggestion with 10 minutes. Each case states, and so overrides, the inputs it tests.

**Test type.** Cases are either function tests (they call the pure recommendation function, and an explanation-builder for the switch lines) or flow tests (they check app behavior). Flow tests are 17 (the function-level part is check 34), the timer part of 18, 20, 30, 31 and 47 to 49; all other cases are function tests. Cases 7, 8, 12, 27 and 28 were revised (same IDs) because the 15-minute standing session made no-equipment and no-floor strength possible; case 29 states its setup as chair only because floor space counts as standing space.

| # | Inputs | Expected result |
|---|---|---|
| 1 | Strength, 20, dumbbells, floor and chair, medium energy, somewhat rested, moderate | S20, tier 2 on every slot, match line shown |
| 2 | Same as 1 with low energy | S20, tier 1 suggested on every slot, lighter-suggestion line shown, user can switch any slot that has another available version |
| 3 | Strength, 30, dumbbells, high energy, well rested, challenging | S30, tier 3 where it exists, dead bug at base with the single-version line, effort line shown |
| 4 | Gentle effort, high energy, well rested, strength 20 | S20, tier 1 on every slot, effort line shown (not the lighter-suggestion line) |
| 5 | Challenging effort, low energy, strength 20 | Tier 1 suggested, lighter-suggestion line shown because energy lowered it |
| 6 | Low energy, strength 30 | Squat, hinge, press and row at tier 1, dead bug at base, lighter-suggestion and single-version lines shown |
| 7 | Strength, 20, no equipment, default setup | B15 recommended with the shorter-than-time line; Squat, Hinge and Press at tier 2; G10 alternative |
| 8 | Strength, 20, no equipment, setup floor, standing and table (no chair) | B15 recommended; Squat and Hinge say "has one version for now"; Press offers base and harder; no G10; no sit-to-stand |
| 9 | Strength, 20, dumbbells, floor space, stable table but no chair | S20 eligible; seated row alternative and G10 not offered |
| 10 | Gentle, 20 or 30, stable chair available (rules test only) | G10 offered with the shorter-than-time line |
| 11 | Gentle, stable table only, no chair | M4, no session offered |
| 12 | Strength, 20, no floor space, standing, chair and table available | S20 not eligible; B15 recommended with the shorter-than-time line; G10 alternative |
| 13 | Open to suggestion, 10 minutes, stable chair available | G10 recommended, no strength alternative shown |
| 14 | Open to suggestion, 10 minutes, no stable chair | M4 (strength line "Our shortest strength session is 15 minutes."; gentle line "The 10-minute gentle session needs a stable chair.") |
| 15 | Open to suggestion, 20, low energy, gentle effort, full setup | G10 recommended, S20 shown as alternative |
| 16 | Open to suggestion, 20, low energy, gentle effort, no stable chair | S20 recommended with easier versions suggested, no G10 alternative |
| 17 | Challenging effort, low energy, user raises one exercise to tier 3 | Allowed; the override line replaces the tier, soreness and single-version lines while the switch is active; no block (function-level check: 34) |
| 18 | More breaks chip on S20 | Rest timer 2:00; time estimate updates |
| 19 | All optional inputs skipped | A recommendation is still produced |
| 20 | Reflection: effort harder than wanted | Easier-versions tip shown |
| 21 | Soreness lower | Squat and hinge suggested at tier 1 with the soreness line; other slots follow capacity |
| 22 | Strength at 10 minutes (only if the duration filter is bypassed) | M1 if G10 is eligible; otherwise M4 (its strength time line now reads "15, 20 or 30 minutes") |
| 23 | Soreness both, strength 30, medium energy, somewhat rested, moderate | Squat, hinge, press, row at tier 1; dead bug at base with the single-version line; soreness line names only the four exercises lowered |
| 24 | Soreness lower, Gentle effort, strength 20 | Tier 1 from effort, effort line shown; no soreness line because soreness lowered nothing |
| 25 | Open to suggestion lands on G10 with soreness upper and More breaks | G10 shown; no soreness line; no rest timer change |
| 26 | More breaks on S20 with 20 minutes chosen | S20 stays eligible; estimate about 23 min shown with a neutral note |
| 27 | Strength, 20, no dumbbells and no floor space, standing, chair and table available | B15 recommended with the shorter-than-time line; G10 alternative |
| 28 | Strength, 20, dumbbells, setup stable table only (no floor, standing or chair) | M4 reading "Strength needs standing space. The 10-minute gentle session needs a stable chair." (dumbbells not mentioned) |
| 29 | Gentle, 10, setup stable chair only (no floor space, no standing space) | G10 without the two standing exercises, about 8 min, shorter-than-time line shows 8 (expectation unchanged; the setup is now stated as chair only because floor counts as standing space) |
| 30 | Reflection after G10: effort harder than wanted | No easier-version tip; skip-or-fewer-repeats tip shown |
| 31 | Stop after exercise 2 of 4 on S20 | Reflection with "Thanks for trying this" and "You stopped after exercise 2 of 4" |
| 32 | Same as 1 with challenging effort (medium energy, somewhat rested) | S20, tier 2 (base) on every slot; lighter-suggestion line shown, naming energy medium, somewhat rested and the base version; effort line not shown |
| 33 | Gentle, 10 minutes, default setup (standing space available) | G10 shown at 10 min, match line exact, no shorter-than-time line |
| 34 | Challenging effort, low energy (suggested tier 1), Press switched to tier 3 (function part of case 17) | One line: "You switched Press to harder. The rest stay as suggested."; lighter-suggestion, soreness and single-version lines hidden; match line stays; switching Press back to tier 1 restores the original lines |
| 35 | Defaults, Squat switched to tier 3 and Row to tier 1 | "You switched Squat to harder and Row to easier. The rest stay as suggested." |
| 36 | Defaults, Squat on its alternative movement; then also Row switched to tier 3 | "You switched Squat to a different movement. The rest stay as suggested."; then "You switched Squat to a different movement and Row to harder. The rest stay as suggested."; switching Squat back to the usual movement restores the original lines (or the single-switch line for Row) |
| 37 | Case 1 inputs, G10 chosen as the session via "Choose this instead" | G10 shown with the fallback match line; S20 shown as the alternative |
| 38 | Strength, 15, defaults | B15 (S20 is longer than 15); exact match line "This matches your 15 minutes, standing space and your preference for strength."; Squat, Hinge, Press at tier 2; G10 alternative |
| 39 | Strength, 20, dumbbells, setup floor only | B15 with the shorter-than-time line; Squat and Hinge offer base and harder (goblet squat, dumbbell Romanian deadlift), suggested base; only Press has one version ("has one version for now"); no G10 |
| 40 | Strength, 15, no equipment, setup stable chair only | M3 "Our strength sessions need standing space."; G10 offered; one "Edit today's setup" action |
| 41 | Strength, 15, low energy, defaults | Squat tier 1, Hinge tier 2 (with dumbbells harder exists, so no single-version line), Press tier 2 (no tier 1, so clamped up); lighter-suggestion line; no soreness line |
| 42 | Strength, 15, high energy, well rested, challenging, defaults (dumbbells) | Squat tier 3 (goblet squat), Hinge tier 3 (dumbbell Romanian deadlift), Press tier 3 (incline); effort line shown (reads "harder versions where they exist") |
| 43 | Same as 42 with equipment none and setup standing and stable chair only | Press tier 2 only with the single-version line; Squat tiers 1 and 2 available, suggested 2; effort line not shown (nothing got a harder version) |
| 44 | Strength, 15, soreness upper, defaults | Press stays tier 2; no soreness line (it lowered nothing) |
| 45 | Strength, 15, soreness lower, defaults | Squat tier 1; soreness line reads "...easier versions of squat." (exercise names are lower case in that line, as in cases 21 and 23); hinge not named |
| 46 | Strength, 15, More breaks on, defaults | B15 still eligible; about 18 min with the longer-rests note |
| 47 (flow) | Check-in, strength, no equipment, setup stable chair only | 15, 20 and 30 greyed with the library "Needs ..." line for each session; no separate Edit button (the Today's setup card has one); hint line shown |
| 48 (flow) | Check-in, strength, dumbbells, setup floor only | 15 selectable; 20 and 30 greyed with "Strength needs a stable chair or table."; ticking a stable chair in Today's setup enables them without leaving the page |
| 49 (flow) | Any mismatch or nothing-eligible screen | One "Edit today's setup" button opening Today's setup expanded; "Edit my check-in" at the top; "Start another check-in" at the bottom; no "Edit my equipment" or "Edit my setup" |
| 50 | Open to suggestion, 15, low energy, gentle effort, defaults | G10 recommended, B15 alternative |
| 51 | Gentle, 10, setup stable chair and floor only | G10 includes the two optional standing exercises (floor counts as standing space) |
| 52 | Strength, 15, equipment none, low energy, setup standing only (no chair, no table) | Squat, Hinge and Press at their only version with three single-version lines; no lighter-suggestion line (nothing got an easier version) |
| 53 | Strength, 15, dumbbells, setup standing and stable chair | Squat offers tiers 1, 2 and 3; Hinge tiers 2 and 3 |
| 54 | Strength, 15, equipment none, setup standing and stable chair | Squat offers tiers 1 and 2 only; Hinge tier 2 only |
| 55 | Gentle, 10, setup with no stable chair | The gentle 10 time is not available; reason "a stable chair" |
| 56 | Open to suggestion, setup standing only (no chair, no table) | 10 not available (reason "a stable chair"); 15, 20 and 30 available |
| 57 | Open to suggestion, setup stable table or counter only (no floor, standing or chair) | No time available |
| 58 | Open to suggestion, setup stable chair only | All four times available |
| 59 | Strength, 15, defaults, soreness upper | No soreness line (lowered nothing); the no-easier line is shown |
| 60 | Strength, 15, defaults, soreness lower | Squat lowered, soreness line names squat; no-easier line not shown |
| 61 | Strength, 15, no equipment, standing space only, soreness lower | Squat, Hinge, Press at base; no soreness line; no-easier line shown |
| 62 | Strength, 20, defaults, soreness lower, Gentle effort (case 24 inputs) | Tier 1 from effort, no soreness line, no-easier line not shown; with case 59 inputs, a Press tier switch hides the no-easier line and undoing it restores it |
