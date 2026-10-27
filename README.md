# PeriMove — Product case study

A home-workout prototype for women approaching or experiencing perimenopause, built solo during the three-day Lovable SheBuilds hackathon in October 2026.

**[Explore the current prototype](https://perimove.lovable.app)** · **[Contact Ivie on LinkedIn](https://www.linkedin.com/in/ivie-clifford)**

> Exercise content is draft, not professionally reviewed or clinically validated. This repository documents the hackathon version; the live app may evolve. It does not establish health outcomes, adherence or sustained use.

## Start here

- **[Quick summary](case-study/summary.md)** — problem, ownership, key decisions and lessons, with a product overview.
- **[Full case study](case-study/README.md)** — trade-offs, research figures, screenshots and iteration examples.
- **[Research companion PDF](research-companion/PeriMove-research-deck-v2.3.pdf)** — nine-slide findings deck; [text transcript](research-companion/README.md).

## My role

Ivie Clifford — problem framing, research, product decisions, design direction, exercise content, recommendation rules, testing and release decisions. Lovable generated the application code from my specifications. ChatGPT and Claude supported research synthesis, planning, review and documentation. The app uses explicit rules, not AI at runtime.

## Supporting evidence

| Material | Contents |
|---|---|
| [Survey summary](research/survey-summary.md) | Final aggregate counts from 40 self-selected respondents, question denominators and limitations |
| [Recommendation rules](specification/recommendation-rules.md) | Bounded recommendation behavior and known specification discrepancies |
| [Acceptance cases](specification/acceptance-cases.md) | Written cases and historical flow checks; distinct from automated test counts |
| [Library overview](specification/exercise-library-overview.md) | Scope and sourcing limits; raw exercise content excluded |
| [Curated decisions](decisions/decision-log.md) | Decisions, rationale and trade-offs |
| [Screenshots](screenshots/README.md) | Interface evidence and captions |
| [Credits and sources](credits-and-sources.md) | Technique references, media credits and outstanding checks |

## What was checked

Lovable reported 324 passing automated tests and a clean production build for the submitted version. I separately checked the app on my iPhone. Six usability sessions (five with people in or approaching perimenopause), plus a separate product review, informed changes. Some feedback followed prompting, and user retesting did not establish resolution of every issue.

The submitted app milestone is `ea710ad11ce84e6423f4472615d12d69b573020f` (movement-button padding fix). This evidence repo is independent of the private app source repository and does not sync to it.

## Current preparation status

Media sources are recorded in the credits file, including the Welcome-screen imagery and supported-row clip. No license is granted for the material in this repository; third-party media remains subject to its own terms. See credits for source details.

Raw survey rows, participant records, private attribution, contact details and internal preparation logs are excluded.
