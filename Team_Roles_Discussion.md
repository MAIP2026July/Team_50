# Team Roles Discussion - Surgery IQ

**Team:** Adithya Mohan, Deepak Narayanan, Mahender Sivaraman
**Purpose:** Agree on who leads each artefact, how work hands off between members, and how we validate outputs together.

---

## 1. Proposed Role Split

| Member                 | Packet roles                                   | Folders led                                                                        | Supports                                     |
| ---------------------- | ---------------------------------------------- | ---------------------------------------------------------------------------------- | -------------------------------------------- |
| **Adithya Mohan**      | Product strategy lead, PM artefacts / PRD lead | 01 Executive Summary, 02 Product Strategy, 03 PM Artifacts                         | 04 (workflow inputs), 07 (governance claims) |
| **Deepak Narayanan**   | UX and workflow lead, prototype / build lead   | 04 UX Workflow Trust, 09 Prototype MVP                                             | 05 (wiring the model into the prototype)     |
| **Mahender Sivaraman** | Data / evaluation lead, business / risk lead   | 05 Data Model Evaluation, 06 Business Economics Scaling, 07 Ethics Governance Risk | 03 (success metrics)                         |
| **Shared**             | All                                            | 08 AI Collaboration, 10 Team Contribution                                          | -                                            |

---

## 2. Responsibilities by Role

### Adithya - Strategy and PM Artefacts

- Topic Approval Form and Milestone 1 submission
- Vision, JTBD, opportunity matrix, build vs buy view, first wedge
- PRD-lite, feature prioritisation, MVP definition, roadmap with proof gates
- Executive summary and the final recommendation story
- Overall integration and consistency check across folders

### Deepak - UX and Prototype

- Scheduler journey and day board flow
- Wireframes: case view, confidence display, "needs review" flag, override with reason
- HTML prototype showing the core decision loop
- Prototype README: what it demonstrates and what it does not yet prove
- Screenshots or a short demo video

### Mahender - Data, Evaluation, Business and Risk

- Synthetic dataset design or public dataset selection, with assumptions documented
- Surgeon-average baseline vs ML model comparison
- Evaluation metrics and go/no-go thresholds
- Pricing, cost drivers, unit economics and scaling risks
- Bias, privacy, misuse, controls and launch blockers

---

## 3. Key Handoffs and Dependencies

| From     | To       | Handoff                                                        | Needed by                            |
| -------- | -------- | -------------------------------------------------------------- | ------------------------------------ |
| Adithya  | Deepak   | MVP scope and core workflow                                    | Before wireframes                    |
| Adithya  | Mahender | Prediction target and wedge definition                         | Before data design                   |
| Mahender | Deepak   | Model output format (estimate, range, top drivers, confidence) | Before prototype build               |
| Mahender | Adithya  | Metrics and thresholds                                         | Before PRD and roadmap are finalised |
| Deepak   | All      | Prototype walkthrough                                          | Before the final deck                |

---

## 4. Discussion Points for Our First Call

### Scope and topic

1. Are we all aligned on Surgery IQ with the case duration and schedule-risk wedge?
2. Which two or three specialties should the MVP cover?
3. Does anyone have concerns about the Topic Approval Form before we submit it?

### Roles

4. Does the role split match each person's strengths and availability?
5. Should anyone swap roles? For example, should Mahender lead UX if he has a stronger design background?
6. Who acts as the backup for each lead if someone is unavailable?

### Data and prototype

7. Synthetic data or a public dataset? Who checks that the data is realistic?
8. Prototype approach: plain HTML with a simulated model, or HTML calling a small trained model?
9. Will we host the repo and live demo publicly? If so, where?

### Ways of working

10. Weekly sync day and time (30 minutes)
11. Shared repo and folder access for all three members
12. Everyone logs AI use weekly in the AI Collaboration Log
13. Peer review rule: every artefact is reviewed by at least one other member before it is marked final

---

## 5. Working Agreements

| Agreement           | Detail                                                                                             |
| ------------------- | -------------------------------------------------------------------------------------------------- |
| Ownership           | The lead drafts, one peer reviews, and the team signs off at milestones                            |
| AI use              | Allowed for drafting and coding; decisions on scope, risk, launch and pricing are made by the team |
| AI logging          | Each member adds entries to folder 08 every week                                                   |
| Data                | Synthetic or public only; no proprietary or patient data                                           |
| Branding            | Surgery IQ is fictional; no real company names, metrics or screenshots                             |
| Contribution record | Each member updates folder 10 with what they led and built                                         |

---

## 6. Milestone Ownership

| Milestone                       | Deliverables                                          | Lead               | Reviewers        |
| ------------------------------- | ----------------------------------------------------- | ------------------ | ---------------- |
| M1 - Topic and Strategy Freeze  | Topic form, vision, JTBD, build vs buy                | Adithya            | Deepak, Mahender |
| M2 - Artefact Review            | PRD draft, wireframes, MVP, roadmap, data assumptions | Adithya and Deepak | Mahender         |
| M3 - Evaluation and Risk Review | Metrics, economics note, risk note                    | Mahender           | Adithya          |
| Final Submission                | Full package, deck, prototype                         | All                | All              |

---

## 7. Decisions Log

| Date        | Decision                                                                | Contributors     |
| ----------- | ----------------------------------------------------------------------- | ---------------- |
| 03 Oct 2026 | Product: Surgery IQ, a fictional surgical intelligence platform         | Adithya/Mahender |
| 10 Oct 2026 | MVP wedge: case duration and schedule-risk assistant for OR schedulers  | Deepak/Mahender  |
| 17 Oct 2026 | Faculty folder structure plus 09 Prototype MVP and 10 Team Contribution | Adithya/Deepak   |
| 24 Oct 2026 | Role split as listed in section 1                                       | All              |
| 31 Oct 2026 | Document Preparation and initial Upload                                 | All              |
| 01 Nov 2026 | Document upload in portal                                               | All              |
