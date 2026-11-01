## PM Artifact Pack - Surgery IQ

**Team 50** | Lead: Adithya Mohan | Reviewers: Deepak Narayanan, Mahender Sivaraman

This pack holds the core PM documents for Surgery IQ. Section 9 shows **how each standard artifact changes because the product is AI-powered**. The full PRD will be in `Appendix/PRD/`.

---

## 1. Problem Statement

> **OR schedulers** in a mid-size hospital **cannot reliably estimate how long each elective case will take** when they book it. They rely on surgeon-requested times or simple averages that ignore patient and case factors. **This causes** room overruns, staff overtime, idle OR time and same-day cancellations. **The decision being improved** is the scheduler's booking decision: *how many minutes to book for this case, and is this room-day at risk?*

What we are **not** solving: automatic booking, block reallocation, emergency case scheduling or surgeon performance assessment.

---

## 2. Product Vision

Every OR day is planned on realistic case estimates, so surgical teams start on time, rooms are not left idle and patients are not cancelled on the day. Surgery IQ delivers this as an embedded intelligence module inside the scheduling tools hospitals already use.

---

## 3. PRD Summary

| Element            | Details                                                                                                         |
| ------------------ | --------------------------------------------------------------------------------------------------------------- |
| **User problem**   | Booking durations are guesses; overruns and idle time are only seen on the day                                  |
| **Primary user**   | OR scheduler                                                                                                    |
| **Secondary user** | Surgical services manager                                                                                       |
| **Where it lives** | Embedded panel inside the existing scheduling screen (simulated in the MVP)                                     |
| **In scope**       | Case duration estimate, likely range, top factors, confidence routing, room-day risk flag, override with reason |
| **Out of scope**   | Emergency cases, auto-booking, block reallocation, surgeon comparisons, GenAI Q&A                               |

### Core workflow

1. Scheduler opens a case request in the existing scheduling screen
2. Surgery IQ pulls case inputs (procedure, surgeon history, patient factors, case order)
3. Model returns predicted minutes, likely range, confidence level and top 3 factors, next to the surgeon-average baseline
4. Room-day risk is recalculated using all cases booked in that room
5. Scheduler accepts, adjusts or overrides the estimate; a reason is required for adjust or override
6. The decision is logged and the manager reviews flagged room-days before the day starts

### AI role

| AI capability        | What it does                                                    |
| -------------------- | --------------------------------------------------------------- |
| Prediction (primary) | Estimates case duration in minutes, with a likely range         |
| Classification       | Flags room-days at risk of overrunning                          |
| Explanation          | Shows the top factors behind each estimate                      |
| Recommendation       | Suggests a booking duration and highlights cases needing review |

**Data assumptions:** Inputs are procedure, specialty, anonymised surgeon ID, surgeon's past average, patient age, BMI, ASA class, anaesthesia type, case order and weekday. The MVP uses synthetic data only, clearly labelled.

### Risks

- Under-prediction overloads a room and pushes later cases back
- Estimates are misused to judge individual surgeons
- Schedulers over-rely on the estimate and stop questioning it
- Accuracy drops as surgical practice or staffing changes

### Fallback logic

| Situation                                                | Behaviour                                                        |
| -------------------------------------------------------- | ---------------------------------------------------------------- |
| High confidence                                          | Estimate pre-filled; one-click accept                            |
| Medium confidence                                        | Estimate shown with range and factors; scheduler confirms        |
| Low confidence (rare procedure, new surgeon, wide range) | "Needs review" flag; defaults to surgeon-average baseline        |
| Model unavailable or input data missing                  | Baseline shown with a "baseline only" label; booking never stops |

*Exact confidence cut-offs will be set in 05_Data_Model_Evaluation.*

---

## 4. User Stories

User stories for an AI product must account for uncertainty, trust and the cost of error.

| #   | As a...      | I want...                                         | So that...                            | Acceptance criteria                                            |
| --- | ------------ | ------------------------------------------------- | ------------------------------------- | -------------------------------------------------------------- |
| US1 | Scheduler    | A predicted duration and range when I book a case | I book realistic time                 | Estimate, range and baseline appear on case selection          |
| US2 | Scheduler    | To see why the estimate differs from the baseline | I can trust or question it            | Top 3 factors shown in plain language                          |
| US3 | Scheduler    | Low-confidence cases flagged clearly              | I do not rely on a weak estimate      | "Needs review" shown; defaults to baseline                     |
| US4 | Scheduler    | To accept, adjust or override with a reason       | I stay in control                     | All three actions work; reason required for adjust or override |
| US5 | Manager      | To see which room-days are at risk                | I can rebalance before the day starts | Day board flags at-risk rooms with contributing cases          |
| US6 | Scheduler    | The screen to keep working if the model fails     | Booking never stops                   | Baseline shown with "baseline only" label                      |
| US7 | Product team | Override reasons captured                         | We can review and retrain the model   | Overrides logged with reason, role and timestamp               |

---

## 5. Feature Prioritization

| Feature                                     | User Value | Effort | Confidence | Priority                            |
| ------------------------------------------- | ---------- | ------ | ---------- | ----------------------------------- |
| Case duration prediction with range         | High       | Medium | High       | **Must have (MVP)**                 |
| Room-day overrun risk flag                  | High       | Medium | High       | **Must have (MVP)**                 |
| Confidence routing and fallback to baseline | High       | Low    | High       | **Must have (MVP)**                 |
| Override with reason capture                | High       | Low    | High       | **Must have (MVP)**                 |
| Top factors explanation                     | Medium     | Low    | High       | Should have                         |
| Plain-language explanation using an LLM     | Medium     | Low    | Medium     | Could have                          |
| Block release recommendation                | High       | High   | Medium     | Phase 2                             |
| Turnover time prediction                    | Medium     | Medium | Medium     | Phase 2                             |
| GenAI Q&A on OR performance                 | Low        | Medium | Low        | Later                               |
| Surgeon comparisons or rankings             | Low        | Medium | Low        | **Excluded** - bias and misuse risk |

*Priority is consistent with the RICE check in 02_Product_Strategy. The team review on 01 Nov 2026 confirmed the room-day risk flag as a Must have.*

---

## 6. MVP Definition

The MVP is successful if it can:

- predict case duration better than the surgeon-average baseline on held-out synthetic data,
- avoid increasing under-prediction compared with the baseline,
- route low-confidence cases to review correctly,
- flag at-risk room-days before the day starts,
- show that schedulers understand and act on confidence and override.

| Element                    | MVP scope                                                       |
| -------------------------- | --------------------------------------------------------------- |
| Setting                    | One fictional hospital, 6 to 8 ORs, elective cases              |
| Specialties                | Orthopaedics, general surgery, urology                          |
| Screens                    | Case booking panel and next-day OR board                        |
| Data                       | Synthetic only, clearly labelled                                |
| **What it does not prove** | Real hospital accuracy, integration effort, real-world adoption |

---

## 7. Roadmap

| Phase                         | Scope                                                                                                                                                                   | Proof gate to move on                                                                                        |
| ----------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------ |
| **Phase 1: Discovery**        | Workflow mapping, data assumptions, baseline definition                                                                                                                 | Problem and baseline agreed by the team                                                                      |
| **Phase 2: MVP (capstone)**   | Prototype with synthetic data                                                                                                                                           | Model beats baseline on error without increasing under-prediction                                            |
| **Phase 3: Controlled pilot** | 3a. Shadow mode: predictions shown to the team only, not used for booking, at one hospital and one specialty. 3b. Assisted mode: schedulers use estimates with override | Accuracy holds on real data; no major error gap across patient groups; override rate stable; overruns reduce |
| **Phase 4: Scale**            | More specialties and hospitals; Phase 2 modules (block release, turnover)                                                                                               | Integration repeatable; economics positive per hospital                                                      |

*Thresholds for each gate will be set in 05_Data_Model_Evaluation and 06_Business_Economics_Scaling.*

---

## 8. Success Metrics

| Type                            | Metric                                                                                                                                              |
| ------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Product metric (North Star)** | Share of room-days finishing within booked block time (within an agreed tolerance)                                                                  |
| Product metric (model)          | Mean absolute error compared with the baseline; share of cases within the tolerance band                                                            |
| **Business metric**             | Overrun minutes and idle minutes per room-day (simulated); overtime and same-day cancellations in pilot                                             |
| **Trust / guardrail metric**    | Under-prediction rate must not increase; error checked across patient segments; override rate and reason mix; share of cases flagged low-confidence |

### Launch checklist (for any pilot)

| Check                                                    | Owner          |
| -------------------------------------------------------- | -------------- |
| Model beats baseline on held-out data                    | Data lead      |
| Under-prediction and segment error checks passed         | Data lead      |
| Fallback to baseline tested                              | Prototype lead |
| Override logging working                                 | Prototype lead |
| No surgeon comparison visible on any screen              | Product lead   |
| Privacy review and access controls confirmed             | Risk lead      |
| Rollback to baseline in one step                         | Prototype lead |
| Escalation path to the surgical services manager defined | Product lead   |
| Scheduler walkthrough completed                          | UX lead        |

---

## 9. How These Artifacts Change Because Surgery IQ Is AI-Powered

| Standard PM Artifact | What changes in an AI product                          | How Surgery IQ applies it                                                                            |
| -------------------- | ------------------------------------------------------ | ---------------------------------------------------------------------------------------------------- |
| Problem Statement    | Must define the decision or workflow being improved    | Framed around the booking decision, not "surgery analytics" (Section 1)                              |
| Persona / User Story | Must account for uncertainty, trust and error cost     | US3 and US6 cover low confidence and model failure; under-prediction is the costly error (Section 4) |
| PRD                  | Must include data assumptions, fallback logic and risk | Data assumptions, four-level fallback table and risk list (Section 3)                                |
| Roadmap              | Must include staged learning and proof gates           | Shadow mode before assisted mode; each phase has an exit gate (Section 7)                            |
| Metrics              | Must connect model metrics to business outcomes        | Model error linked to overrun minutes, idle time and the North Star (Section 8)                      |
| Launch Checklist     | Must include review, rollback and escalation           | Rollback to baseline, manager escalation and segment checks (Section 8)                              |
| Pricing Note         | Must account for inference or operating cost           | Covered in 06_Business_Economics_Scaling                                                             |
| Review Memo          | Must separate hype from defensible product logic       | MVP claims limited to what synthetic data can show; "does not prove" stated (Section 6)              |

---

*Surgery IQ is a fictional product created for academic purposes. It uses synthetic data only.*
