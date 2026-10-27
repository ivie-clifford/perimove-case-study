# Decision log (curated)

A short trail of the decisions that shaped PeriMove, with the reason and the trade-off for each. It is curated from a longer working log; routine build steps, prompt wording, process notes and participant-level detail are left out. The working log is private.

**Evidence labels.** *Survey* = self-selected stated views (40 responses). *Sessions* = observed confusion in six usability sessions (five with people from the target group) plus a separate product review; counts are small and early records were short summaries. *Tests* = results reported by Lovable for specified behaviors. None of these shows health outcomes, adherence, beginner suitability or product-market fit.

## Product and scope

### 1. Narrow to one daily decision
- **Decision.** Help a woman approaching or experiencing perimenopause decide what movement feels manageable today and how to adapt it. Diagnosis, symptom interpretation, wearables, cycle tracking, nutrition prescriptions, accounts and community are out of scope.
- **Why.** The survey showed uncertainty about adapting workouts (20 of 40 reported low confidence). It was not the strongest request: understanding perimenopause and exercise (23) and strength and muscle (18) were each asked for more often than deciding between a workout, gentle movement or rest (15) or modifying exercises (11). Those last two supported the chosen focus because they are the part a rules-based tool could address directly, while education and a strength program were outside what I could build and review in three days. I chose not to build education.
- **Trade-off.** A narrow product that does not teach, and depends on the person already knowing how she feels.

### 2. Rules, not AI, at runtime
- **Decision.** One written rules function chooses the session and the exercise versions. Explanations are templates filled only from the user's own answers.
- **Why.** For health-adjacent content I wanted behavior I could predict, test and explain. A model could invent exercises or safety judgments I could not check.
- **Trade-off.** Less flexibility and a small fixed set of sessions. The specification became the central artifact (see `specification/`).

### 3. The user sets the ceiling
- **Decision.** The effort the person chooses is the maximum. Energy and rest can only suggest something lighter, with a one-line reason; on the recommendation screen she can switch an exercise to another available version or a named alternative movement, and during a strength session she can change the level of the current exercise for its remaining sets. She can pause, skip or stop on the guided screens, and add rest in strength sessions, with no penalty wording. Not every control is everywhere: the gentle session has one level, exercises with one available version have no switch, and alternative movements are chosen before the session starts.
- **Why.** No clinical basis for silent calls about someone's body; she is the expert on her own day.
- **Trade-off.** More conservative and less "smart". Known gap, deferred: no nearby explanation appears when several causes overlap.

### 4. Account-free, with data kept on the device
- **Decision.** No accounts, history or name field. The saved setup stays in the browser; check-in and reflection answers are memory-only and are not sent to a server.
- **Why.** A backend adds security surface and sign-up friction, and there was no multi-week plan yet for an account to hold. A name field was tried and removed because it felt like another form.
- **Trade-off.** No history, resume or cross-device use.

### 5. Treat the content as unreviewed, and limit it to what could be sourced
- **Decision.** All exercise content is labeled as prototype content that has not been professionally reviewed. Movements were included only where a credible technique reference existed.
- **Why.** I could not claim clinical validity, so the honest design was a small, clearly labeled library and a visible label on guided screens.
- **Trade-off.** Several slots have only one version and some useful movements are missing. See `specification/exercise-library-overview.md`.

## Recommendation logic

### 6. A standing session instead of "no equipment, no session"
- **Decision.** Add a 15-minute standing strength session (squat, hinge, press) so that a person without dumbbells, floor space or a table still gets a real option. It has no pulling movement, so it is not called full body.
- **Why.** A person with floor space and dumbbells but no table or chair reached a dead end twice during checks, although three of the four movements needed no surface.
- **Trade-off.** A fourth session to maintain; some versions only appear when the setup allows them.

### 7. Show what is unavailable instead of letting people hit a dead end
- **Decision.** On the check-in, times that cannot run with today's setup are greyed out with the reason ("Needs a stable chair"). The "nothing fits" screen became a safety net, and every mismatch screen lists the unmet needs from the user's own answers and offers one "Edit today's setup" action.
- **Why.** Checks reached the nothing-fits screen from Gentle and Open to suggestion; preventing the dead end is kinder than explaining it.
- **Trade-off.** More states to specify and test (cases 47 to 58 in `specification/acceptance-cases.md`).

### 8. Soreness only lightens, and the screen says so only when it did
- **Decision.** Soreness (upper, lower or both) can lower the suggested version of affected exercises. A soreness line appears only when it actually changed something; a separate line says when no easier version exists for a sore area.
- **Why.** Soreness is not pain and no screen interprets it. A line that claimed an effect that did not happen would be misleading.
- **Trade-off.** Some answers produce no visible change.

### 9. Switching must never mislead
- **Decision.** While any version or movement switch is active, the lines that describe the original suggestion are hidden and one line names exactly what was switched.
- **Why.** Those lines describe variants that are no longer all in place and would be wrong.
- **Trade-off.** The explanation changes as the user changes the plan.

## What testing changed

These changes came from observed confusion in the usability sessions and a separate product review. The records show the changes were built and checked by the builder; they do not establish that each issue was resolved in user retesting.

### 10. Separate the preview from the workout
- **Observed.** People confused the preview with the workout and missed or hesitated at Start.
- **Change.** A clearer "Today's workout" summary, a pinned Start, a single "Change today's answers" action and more distinct journey stages.

### 11. Allow more than one reason in the reflection
- **Observed.** A single reflection reason could not capture several things that went wrong.
- **Change.** Multiple reasons and an optional short note, kept in memory only.

### 12. Make versions and alternative movements distinguishable
- **Observed.** Exercise versions and alternative movements were hard to tell apart; customization could be lost when switching to a gentle session and back.
- **Change.** Clearer labels, explanations and named switching and return actions; changed check-in answers reset prior customization while no-op edits preserve it.

### 13. Replace "Demonstration pending" with a clearer placeholder
- **Observed.** The pending label confused people, and several valued the idea of video.
- **Change.** Five short demonstrations and "Video coming soon" placeholders for the rest. A demonstration shows a movement; it does not validate technique or suitability.

### 14. Keep Stop reachable and the layout phone-first
- **Found during checks.** Stop scrolled out of view on some rest screens; the prototype notice and controls were crowded on small screens.
- **Change.** A shared guided header intended to keep Stop visible on every guided screen, and a timer-first layout.
- **Still open.** On a short phone screen the first strength view needs scrolling; the cause is unresolved.

## Process decisions

### 15. Keep prompts small, and list every test a wording change affects
- **Why.** Long pasted prompts were cut off by the build tool, and a wording change once broke an existing test because the prompt did not list that test as a permitted update.
- **Rule adopted.** Keep each prompt short, ask the tool to quote the last line it received, and list every test that asserts changed wording.

### 16. Freeze for judging, then keep the submission as a milestone
- **Decision.** The prototype was frozen while it was being judged, and the frozen version was recorded as the submitted version. The judging freeze has ended: the submitted version remains a historical milestone, and the evidence in this repository describes it, but development of the app can continue and the live app may change from here. The app's source repository stays private, and evidence is published separately in this repository.
- **Why.** The app repository holds generated files and a long automatic history that add risk and little value if public. Keeping the submitted version identifiable lets the evidence here be checked against a fixed point.
- **Trade-off.** Documents here can drift from the live app as it evolves; each one should say which version it describes.

## Still open
- Professional review of the exercise content (none arranged).
- Whether the explanation gap for overlapping causes should be closed.
- Repeated-use testing over several days (not done).
- An earlier explanation of the experience for first-time visitors, and equivalent mobile and desktop refinement (from the builder's own review after submission, not from the formal sessions).
- Short-screen scrolling on the strength first view.
