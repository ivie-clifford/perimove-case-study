# PeriMove: adapting a home workout to how you feel today

**What it is.** PeriMove is a web app that helps women approaching or experiencing perimenopause adapt a home workout to how they feel today. I built the prototype solo during the three-day Lovable SheBuilds hackathon in October 2026. I led the research, product decisions, design direction, exercise content and testing. I used Lovable to build the app, with ChatGPT and Claude supporting research synthesis, planning and review.

Explore the current prototype: https://perimove.lovable.app

<table>
<tr><th>1. Check in</th><th>2. Review and adapt</th><th>3. Follow the guidance</th></tr>
<tr>
<td width="33%" valign="top"><a href="../screenshots/PeriMove_Checkin_Controls.png">
  <img src="../screenshots/PeriMove_Checkin_Controls.png" alt="Choose today’s effort and optional adjustments." width="220">
</a></td>
<td width="33%" valign="top"><a href="../screenshots/PeriMove_01_Workout_Preview.png">
  <img src="../screenshots/PeriMove_01_Workout_Preview.png" alt="Review suggested versions and change available choices. Extended page view." width="220">
</a></td>
<td width="33%" valign="top"><a href="../screenshots/PeriMove_02_Guided_Squat.png">
  <img src="../screenshots/PeriMove_02_Guided_Squat.png" alt="Use written cues, Listen and movement demonstrations." width="220">
</a></td>
</tr>
<tr>
<td valign="top"><sub><em>Choose today’s effort and optional adjustments.</em></sub></td>
<td valign="top"><sub><em>Review suggested versions and change available choices. Extended page view.</em></sub></td>
<td valign="top"><sub><em>Use written cues, Listen and movement demonstrations.</em></sub></td>
</tr>
</table>

*Illustrative screens from the daily journey, not a recording of one continuous session. Exercise content is prototype content and not professionally reviewed.*

**The problem.** Exercise plans can be hard to adapt when every day feels different. For many women in perimenopause, energy, recovery and symptoms can vary, and general advice is hard to turn into a decision on the day: follow the workout, make it easier, choose gentler movement or rest?

**What I heard.** In a self-selected survey of 40 people, 28 said they were approaching or experiencing perimenopause, and 20 of 40 reported low confidence adapting a workout when they felt different. Of the 39 respondents who answered the multiple-choice support question, understanding perimenopause and exercise was the largest request (23), followed by strength and muscle (18), choosing between a workout, gentle movement or rest (15), and modifying exercises (11). These findings supported testing a tool for daily workout adaptation.

**What I built. **My longer-term ambition was to help women build consistency with training that evolves over time. For the three-day hackathon, I focused on adapting today’s workout: onboarding, a daily check-in, an adjustable workout preview, a guided session and reflection. I deferred broader education about perimenopause and exercise because of the time constraint and because I had not secured enough expert sources or professional review to support it. I did include a small set of source-linked general tips on consistency, strength and recovery. A fixed rule chose the tip from saved goals, with a session-type fallback; it was not ongoing coaching or a broader education feature.

I kept it account-free, with setup saved in the browser so people wouldn’t have to answer the same setup questions each visit. Workout history and ongoing plans were deferred; the prototype doesn’t learn from previous sessions or adjust training across weeks.

**Four decisions that shaped it**

1. **Keep the user in control.** The user’s chosen effort sets the ceiling for the recommendation. Energy and rest can suggest something lighter, while users can change exercise choices and control their rest. Where supported, explanations connect suggested changes to their answers.
2. **Rules, not AI, at runtime.** Recommendations follow explicit rules and use predefined explanations. That made the behavior predictable and easier to inspect and test within three days.
3. **Treat content as unreviewed.** Exercises are limited to movements with a credible technique source, labeled as prototype content, and not presented as clinically validated. The cost was a deliberately small library.
4. **Let observed use reshape the journey.** Six usability sessions (five from the target group) and a separate product review informed a redesigned recommendation page, a clearer pre-workout journey, multi-select reflection, voice guidance and demonstration clips.

**How it was checked.** Lovable reported 324 passing automated tests and a clean production build. I separately checked the app on my iPhone. Usability sessions surfaced specific improvements to the flow and controls. These checks did not evaluate continued use or health outcomes.

**What I would do differently.** Add a short orientation before the check-in so a first-time visitor understands the experience without explanation, and design for desktop as well as mobile from the first prompt so the experience works well on either device. 

**What is next.** Professional review of the exercise content and a multi-day test with real routines. The longer-term vision includes training that adapts across perimenopause and education about perimenopause and exercise, supported by expert sources and professional review.
