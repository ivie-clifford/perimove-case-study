# PeriMove recommendation rules

> **Status.** Specification of the prototype's rules-only recommendation logic, written for and checked against the prototype submitted in October 2026 (https://perimove.lovable.app). It is a historical record of that version: development can continue, and the live app may change. These are usability and matching rules, **not clinical rules**. No symptom is interpreted, nothing is diagnosed or predicted, and **no rule or exercise has been professionally reviewed**. Tier thresholds, the capacity rule and the soreness rule are unreviewed product proposals made for flow testing; they would need professional review before any public release.
>
> This file began as a working specification during the build, so some wording is older than the submitted app. Section 10 lists the details that were checked against the submitted build (its library and automated tests) and the discrepancies that remain; where screen wording differs from a template below, the submitted app is the record. A known gap, deferred: no nearby explanation is shown when several causes overlap. The acceptance cases are in [acceptance-cases.md](acceptance-cases.md); the exercise library is described in [exercise-library-overview.md](exercise-library-overview.md).

## 1. Principles
- Rules only; no AI selects or generates anything in v1. The explanation line is a template.
- Curated content only: unreviewed in the prototype, reviewed before any public release. If nothing fits, explain the mismatch and offer only eligible choices.
- Desired effort is the user's ceiling. Energy and rest can only suggest something lighter, never heavier.
- Within the controls each screen offers, the user can change a version or alternative movement, pause, skip, stop or add rest, with no penalty wording. Not every control appears on every screen (see section 10).
- Nothing here diagnoses, treats or predicts anything.

## 2. Session library (v0.4)
| ID | Session | Duration | Needs | Status in the submitted build |
|---|---|---|---|---|
| S20 | Strength, 4 movements | 20 min | Dumbbells; floor space; stable chair or table | Built; draft content (unreviewed). The app's clip list includes a supported-row clip |
| S30 | Strength, 5 movements (adds dead bug) | 30 min | Same as S20 | Built; draft content (unreviewed). Dead bug has one version; the clip list includes a dead bug clip |
| B15 | Standing strength, 3 movements (squat, hinge, press) | 15 min | Standing space (floor space counts); no equipment, no floor; a free wall is assumed. The mini-squat and sit-to-stand need a stable chair; the incline push-up needs a table or counter | Built; draft content (unreviewed); written cues. Which of its movements show a clip or the "Video coming soon" placeholder was not checked in this pass (see section 10) |
| G10 | Gentle mobility and relaxation | 10 min | Stable chair (no wheels or arms); two optional standing exercises | Built; draft content (unreviewed). The clip list includes a standing side bend clip |

## 3. Step 1: eligibility filters (applied in order)
| Check | Rule | If it fails |
|---|---|---|
| Needs | S20 and S30 need dumbbells, floor space and a stable chair or table. B15 needs standing space only (floor space counts as standing space). G10 needs a stable chair (no wheels or arms). A table alone makes S20 and S30 eligible but not G10. | M3 if no strength session fits; M4 if nothing is eligible |
| Type and time | A session is time-eligible only if it is no longer than the time chosen. Strength times are 15, 20 and 30: 15 gives B15, 20 gives S20 (or B15 if S20's needs are unmet), 30 gives S30 (or S20, or B15). Gentle: G10 at any time. | M1 |
| Open to suggestion | See step 2 | n/a |

A session is eligible when its needs are met and it is no longer than the time chosen. Alternatives and mismatch options come only from eligible sessions, with at most two shown. When a shorter session of the chosen type fits inside the time given (for example gentle with 30 minutes), offer it and say it is shorter than the time available. Never stretch a session to fill time.

**Setup terms:** a stable chair is one you can sit on (no wheels or arms); a stable surface is a table, counter or sturdy chair you can lean a hand on. A chair counts as both. Standing space is room to stand and move; floor space counts as standing space. It gates B15 and G10's two optional standing exercises, which are omitted when it is not met. A table or counter (the "Stable table or counter" option) is separate from a chair: the incline push-up needs the table or counter, and a chair alone does not meet it. A free stretch of wall is assumed, not asked (used by the wall push-up alternative). In the rules, "stable chair or table" for strength means a stable surface; the gentle session and the seated row alternative need a stable chair.

## 4. Step 2: choosing a session when the user is open to suggestion
1. Find eligible sessions: needs met and no longer than the time chosen.
2. If none is eligible, show M4. If some session is eligible but none of the chosen type, show M1, M2 or M3 (section 7).
3. Open to suggestion with 10 minutes: only G10 can fit, because strength sessions are 15, 20 and 30 minutes. Open to suggestion offers 10, 15, 20 and 30. Recommend G10 if a stable chair is available; otherwise show M4. No strength alternative is shown.
4. If capacity is Low and desired effort is Gentle: recommend G10 if it is eligible, and show the longest eligible strength session as an alternative if there is one. If G10 is not eligible, recommend the strength session.
5. Otherwise recommend the longest eligible strength session (S20, S30 or B15), with G10 as an alternative only if it is eligible. A strength session is never offered as the alternative to another strength session.
6. If only one session is eligible, recommend it, explain why, and show no alternative.

## 5. Step 3: variant tier for each exercise
**Capacity** comes from energy and rest only:
| Energy | Rest | Capacity | Highest suggested tier |
|---|---|---|---|
| Low, or | Not rested | Low | 1 (easier) |
| High and | Well rested | High | 3 (harder) |
| Anything else | | Medium | 2 (base) |

**Effort ceiling:** Gentle = 1, Moderate = 2, Challenging = 3.
**Suggested tier = the lower of the effort ceiling and the capacity cap.** Examples: challenging effort with low energy suggests tier 1; gentle effort with high energy and rest still suggests tier 1; moderate with high capacity suggests tier 2.
**Tiers depend on today's setup.** A tier is available only if its needs are met (B15: the mini-squat needs a stable chair; the incline push-up needs a table or counter). The suggested tier is clamped to the nearest available tier of that slot (ties go to the lower); B15's squat has tiers 1 (needs a chair), 2 and 3 (goblet squat, needs dumbbells), its hinge tiers 2 and 3 (dumbbell Romanian deadlift, needs dumbbells), its press tiers 2 and 3 (incline, needs a table or counter). A tier that needs dumbbells is available only when today's equipment is dumbbells. Easier and Harder show only for tiers that are available. Slots with a single available tier (dead bug; B15's hinge; B15's squat or press when its extra tier is unavailable) use that version, show no switch, and say it has one version for now. The single-version line names the slot (Squat, Hinge, Press), except the dead bug, which keeps its own name, and it appears whenever exactly one version is available even if a different movement is also offered. Every slot offers an easier and harder switch where a variant exists. The user may select any tier, including above the suggested one, with no block or warning beyond a neutral note.

## 6. Optional inputs
| Input | Rule | Status in the submitted build |
|---|---|---|
| Soreness: upper | Press and row suggested at tier 1 | Built |
| Soreness: lower | Squat and hinge suggested at tier 1 | Built |
| Soreness: both | Every slot that has an easier version suggested at tier 1; single-version exercises stay at base | Built |
| Soreness: none or not sure | No effect | Built |
| More breaks (chip) | Rest timer defaults to 2:00; the time estimate is recalculated and shown (S20 becomes about 23 min; S30 stays under 30). Eligibility uses the labelled duration, so the session is not re-filtered; a neutral note shows the longer estimate | Built |
| Simpler instructions (chip) | Show one short cue per exercise instead of the full set | Built |

Soreness is treated as lighter-variant guidance only. It is not pain, and no screen interprets it. The soreness line names only exercises whose final suggested tier it actually lowered (after clamping); it is not shown when effort is already Gentle or when the session is G10 (single level). The earlier "shorter session" and "standing-only" chips are dropped. **Controls by type:** when gentle is chosen, Soreness and More breaks are hidden, because G10 has one level and no timed rests. Open to suggestion shows all optional controls and ignores any that do not apply to the session recommended.

## 7. Mismatch states
Each mismatch screen names every unmet need for the chosen type in plain words, offers at most two eligible options, and never generates a workout.

**Precedence:**
1. Build the eligible set across all sessions: needs met and no longer than the time chosen.
2. If it is empty, show M4, whichever check failed.
3. If it is not empty but the chosen type has no eligible session, show M1 (time), M2 (equipment) or M3 (space). If more than one applies, one screen names every unmet need.
4. Otherwise, recommend.

| ID | Trigger | Message intent | Options |
|---|---|---|---|
| M1 | No session of the requested type fits the time chosen (not reachable with type-first ordering; a safety net) | "We don't have a [type] session for [time] yet." | G10 if eligible; otherwise none (see M4) |
| M2 | Retired during the build (strength no longer needs dumbbells: B15 is bodyweight) | n/a | n/a |
| M3 | Strength requested, no strength session fits, G10 is eligible. One screen for every strength mismatch | "Our strength sessions need [unmet_list]." (the submitted app and its test use "Our"; an earlier draft said "These"). The list comes from the closest-fitting strength session: among those no longer than the time chosen, the one with the fewest unmet needs (ties go to the shorter) | G10; one "Edit today's setup" button |

**M4:** nothing is eligible, whichever check failed. The screen lists each session's actual unmet needs, built from the user's own inputs and never hard-coded, for example "Strength needs standing space. The 10-minute gentle session needs a stable chair." The title reads "We don't have a session for these choices yet." When time is the reason: "Our shortest strength session is 15 minutes." The message ends with one closing line: "Choose more time, or update today's setup if you have a suitable chair." when the time chosen is under 15 minutes and B15's needs are met for today's setup (more time would unlock a session); otherwise "Update today's setup to see what's available." It offers one "Edit today's setup" button (plus Edit my check-in at the top and Start another check-in at the bottom) and shows no session. Nothing is generated. Because the check-in now greys every time that cannot run (see below), this screen is a safety net that the check-in can no longer reach.
Editing the check-in is always one tap from a mismatch screen.

**Check-in availability.** On the check-in, a time is selectable only if it can run with today's equipment and setup. Others stay visible, greyed out and not selectable, with the library line "Needs [unmet_list]." under them. *Strength:* the strength session of that length must have its needs met (15 is B15, 20 is S20, 30 is S30). *Gentle:* the 10-minute time needs G10's needs met (a stable chair). *Open to suggestion* (10, 15, 20, 30): a time is available if at least one session no longer than it, by labelled length, has its needs met; the unmet list for a greyed time comes from the closest-fitting session no longer than that time (fewest unmet needs; ties go to the shorter), the same rule M3 uses. A greyed time that was already selected is cleared when the setup changes (nothing else is picked for the person). When any time is greyed, a hint line shows (currently "Greyed options need something in today's setup."). There is no separate Edit button; the Today's setup card has one. This prevents the dead end where a person with dumbbells and floor space but no table or chair could pick 20 minutes and reach a mismatch, and the same dead end for Gentle and Open to suggestion. The recommend function still returns the best fitting shorter session if it is called with a duration the setup cannot run (see cases 7, 8, 12 and 27).

## 8. Explanation templates
Templates are filled only from the user's own inputs.
- **Match line:** four variants. Exact match (right type, same length as the time chosen): "This matches your [time] minutes, [setup] and your preference for [type]." Right type but shorter than the time: "This matches your preference for [type] and fits within your [time] minutes." Open to suggestion: "This fits your [time] minutes and what you have today." A different type from the one chosen (for example the gentle session after a strength mismatch, or listed as an alternative): "This is a session we can offer for your setup today." [setup] is dumbbells for strength and a stable chair for gentle. Never claim a session matches a time it is shorter than, or a preference it does not meet.
- **Lighter suggestion** (shown whenever the suggested tier is below the tier the chosen effort asks for because energy and rest set a lower cap; name the tier actually suggested and the energy and rest answers given): "You said your energy is [low / medium / high] and you feel [not rested / somewhat rested / well rested] today, so we suggested the [easier / base] version of each exercise that has one. You can switch any exercise."
- **Effort line** (shown when effort set the suggestion, in place of the lighter-suggestion line): "You chose [effort] effort, so we suggested [easier / base / harder] versions where they exist. You can switch any exercise."
- **No-easier soreness line**: "There isn't an easier version available, with today's setup, for at least one exercise that targets an area you marked sore." Shown in the soreness line's place only for strength sessions when soreness is upper, lower or both, the soreness line is not shown, and at least one sore-area exercise's lowest available version is its base version. Not shown for G10, for soreness none or not sure, or while a switch is active.
- **Soreness line** (shown when soreness lowered specific exercises): Upper: "You said your upper body feels sore, so we suggested easier versions of [exercises]." Lower: "You said your lower body feels sore, so we suggested easier versions of [exercises]." Both: "You said your upper and lower body feel sore, so we suggested easier versions of [exercises]." [exercises] lists only exercises whose suggestion soreness actually lowered, never single-version ones.
- **Tier lines with mixed results:** the effort line and the lighter-suggestion line say "easier" or "harder" only if at least one exercise's suggested version actually is easier or harder than its base; otherwise the line is not shown. Their wording ("each exercise that has one", "where they exist") already covers mixed results such as B15's. A line that says "base" is shown as before.
- **Single-version line:** "[Exercise] has one version for now." The rules function still returns this line and tests check it, but the submitted app does not display it; each single-version exercise card shows the label "Only one level available" instead.
- **Override line**: shown only while the user has switched exactly one exercise to another tier: "You switched [exercise] to [easier / base / harder]. The rest stay as suggested." The exercise is named by its slot label (Squat, Hinge, Press, Row, Core).
- **Switch lines**: a switch is a tier different from the suggested one, or a chosen alternative movement ("Use a different movement"). While at least one switch is active, the effort or lighter-suggestion line, the soreness line and the single-version lines are hidden, because they describe variants that are no longer all in place; the match line and shorter-than-time line stay. Each exercise still shows its "Suggested" marker, and a single-version exercise still shows its one version as a single selected button (replacing an earlier "One version for now" card label). Exactly one tier switch uses the override line above. A movement switch, or more than one switch, uses: "You switched [switches]. The rest stay as suggested." where each switch reads "[exercise] to [easier / base / harder]" or "[exercise] to a different movement", in slot order, joined with commas and "and" (for example "You switched Squat to a different movement and Row to harder. The rest stay as suggested."). Switching back to the suggested tier or the usual movement removes that switch; when none remain, the original lines return.
- **Shorter-than-time line:** "This session is about [n] minutes, shorter than the time you have." [n] is the displayed estimate (about 8 or 10 for the gentle session).
- **Longer-rests note** (when More breaks makes the estimate longer than the time chosen): "With longer rests, this is about [n] minutes." The function still returns this note, but the submitted app shows the session card line "About [n] min with longer rests" instead.
- **Gentle single-level line:** "This session has one gentle level."
No template mentions causes or conditions; templates only repeat what the user entered.

## 9. Reflection rules
| Answer | Result |
|---|---|
| Effort harder than wanted | Tip: consider the easier versions next time, only if an exercise done has an easier version |
| Effort easier than wanted | Tip: consider the harder versions next time, only if an exercise done has a harder version |
| Effort about right | No tip |
| Fit: partly or not well | Show the optional "What didn't work?" question |
| Wants plan to adjust over weeks (yes, maybe, no) | Recorded for testing only; no behavior change |
| Effort harder than wanted (gentle session) | Tip: skip any exercise or use fewer repeats next time. No easier-version tip |
| Effort easier than wanted (gentle session) | No tip |
| Stopped early (any session) | Headline "Thanks for trying this" and a line naming where you stopped; same questions, worded for the part done. If no exercise was completed, skip reflection |
| Done | Closing screen: thanks, come back tomorrow, optional reminder file. Nothing is stored. "Start another check-in" returns to the check-in with answers cleared |

Tips apply to the current visit only. Nothing is stored.

## 10. Reconciliation with the submitted build

Checked on October 26, 2026, read-only, against the submitted version of the app (its content library and automated test files). Test results are as reported by Lovable; they were not re-run in this pass, and this was not a line-by-line audit of the code.

**Confirmed against the submitted build**
- The four sessions, their lengths and needs (S20, S30, B15, G10) and the 15, 20 and 30 strength times match the app's library.
- B15 has three slots (squat three versions, hinge two, press two); S20 has four slots with three versions each; the app's library marks G10 as a single level.
- The retired M2 and combined M2/M3 messages are marked retired in the app's library; M3 serves every strength mismatch.
- The app's library carries the greyed-time lines, "Only one level available" and the all-greyed message in the wording given above, and a test checks the M3 title "Our strength sessions need standing space."
- Five demonstration clips are in the app's clip list (bodyweight squat, supported single-arm row, dead bug, standing side bend, floor bridge); other exercises use the "Video coming soon" placeholder.
- Level switching during a strength session (remaining sets only) is built and tested. It switches levels only: alternative movements are not switched mid-session, and the gentle session has no levels.
- The submitted library shows four general-information tips; the authoring copy held ten, of which seven were marked visible when authored.

**Discrepancies and unresolved items**
1. The M3 title in earlier drafts ("These strength sessions need...") was corrected to the built wording ("Our strength sessions need...") in this file and in case 40.
2. The app's library lists the mismatch actions as "Edit my check-in" and "Edit today's setup", but one constant in the app's rules code still names "Edit my equipment" and "Edit my setup". Which labels appear on screen was not checked in this pass.
3. The app's library still carries an old status flag on B15 ("placeholder", "to_write") for its demonstrations and cues, although cues exist. This is stale metadata; its effect on screen was not checked.
4. Which exact screens show a clip rather than the placeholder for B15's movements was not checked.
5. Cases 59 to 62 and the flow checks (47 to 49 and the screen checks in the acceptance file) were written from the specification; this pass did not map each case to a specific automated test.

