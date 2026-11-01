## Topic Approval Form

**Course:** MBA ZG583 - Management of AI Products

**Assignment:** Experimental Learning Assignment / Capstone

**Milestone:** Milestone 1 - Topic and Strategy Freeze

### Team Name

Team 50

### Team Members

| Name               | Student ID  | Lead Role                                  |
| ------------------ | ----------- | ------------------------------------------ |
| Adithya Mohan      | 2025MB26149 | Product strategy and PM artifacts lead     |
| Deepak Narayanan   | 2025MB26148 | UX / workflow and prototype build lead     |
| Mahender Sivaraman | 2025MB26147 | Data / evaluation and business / risk lead |

### Working Title

**Surgery IQ: An embedded AI case-duration and schedule-risk module for OR scheduling**

Surgery IQ is a surgical intelligence layer that sits on top of existing operating room (OR) scheduling systems. Its first module predicts case duration and schedule risk at the moment a case is booked.

### Industry / Function

Healthcare - hospital surgical operations / OR scheduling

### Target User

| User type     | Who                                  | How they use Surgery IQ                                           |
| ------------- | ------------------------------------ | ----------------------------------------------------------------- |
| Primary       | OR schedulers                        | Book elective cases every day using the predicted duration        |
| Secondary     | Surgical services managers           | Review rooms or days flagged as at risk of overrunning            |
| Beneficiaries | Surgeons, OR nursing teams, patients | Fewer late starts, less overtime and fewer same-day cancellations |

### Current Workflow Problem

- Schedulers book each case using the surgeon's requested time or a simple historical average.
- These estimates do not reflect patient, procedure or team factors, so many cases run longer or shorter than booked.
- Overruns push later cases back, cause staff overtime and can lead to same-day cancellations.
- Underruns leave expensive OR time idle.
- Schedulers get no early warning that a room's day is at risk until it is already running late.

### Why This Matters

- OR time is one of the most expensive and revenue-critical resources in a hospital.
- Booking accuracy directly drives OR utilisation, overtime cost and cancellation rates.
- Late starts and cancellations affect patient experience and timely access to care.
- The booking decision is repeated for every case, every day, so small accuracy gains add up.

### Proposed AI Role

**Prediction**, supported by classification and recommendation.

| AI capability        | What it does                                                                          |
| -------------------- | ------------------------------------------------------------------------------------- |
| Prediction (primary) | Estimates case duration in minutes, with a likely range, from historical patterns     |
| Classification       | Flags rooms or days at risk of overrunning, based on the combined predicted durations |
| Explanation          | Shows the top factors behind each estimate in plain language                          |
| Recommendation       | Suggests a booking duration and highlights cases that need scheduler review           |

### Why AI Instead of a Simpler Alternative

| Alternative            | Why it is not sufficient on its own                                                |
| ---------------------- | ---------------------------------------------------------------------------------- |
| Surgeon average (rule) | One number per surgeon and procedure, so it ignores patient and case variation     |
| Fixed buffer rules     | The same buffer on every case over-books simple cases and under-books complex ones |
| Dashboards / analytics | Explain past overruns but do not estimate upcoming cases                           |
| Process redesign       | Helps, but schedulers still need a better estimate at the moment of booking        |

AI can combine many factors for each case and attach a confidence range. The surgeon average remains the **baseline the model must beat**.

### Human-in-the-Loop Design

- Surgery IQ suggests a duration. It never books or moves a case on its own.
- The scheduler accepts, adjusts or overrides each suggestion and records a short reason.
- Low-confidence cases (rare procedures, new surgeons, limited history) are flagged for manual review and default to the surgeon average.
- The surgical services manager decides on any room or day level changes.
- Override reasons feed back into model review and retraining.

### Smallest Credible MVP

An embedded module, shown inside a simulated scheduling screen for one fictional hospital, covering elective cases in two or three specialties. The scheduler can:

1. Select a case and see its predicted duration and range next to the surgeon-average baseline
2. See the top factors behind the estimate
3. See a confidence level and a "needs review" flag when confidence is low
4. View a day board with rooms at risk of overrunning
5. Accept, adjust or override the estimate and capture a reason

**Data:** Synthetic data only, clearly labelled as synthetic. No real patient data and no proprietary company data.

### Build vs Buy vs API View

**Initial recommendation:** Build the prediction module, use an API for optional explanations, and partner for scheduling system integration.

| Component                     | Path                   | Why                                                                                    |
| ----------------------------- | ---------------------- | -------------------------------------------------------------------------------------- |
| Duration model                | Build (lightweight ML) | Tabular prediction is cheap to train and run, and the inputs are structured            |
| Plain-language explanation    | API (LLM), optional    | Turns model drivers into readable text without building a language model               |
| Scheduling system integration | Partner (later phase)  | Hospitals already schedule in existing systems; Surgery IQ embeds rather than replaces |

The differentiation lies in the workflow: estimates at the moment of booking, confidence routing, the override loop and day-level risk. It does not come from owning a complex model.

### Main Risks

- **Inaccurate estimates:** Under-prediction could overload a room, so low-confidence cases must route to review.
- **Misuse as a surgeon scorecard:** Predictions could be used to judge individual surgeons unfairly. The MVP excludes any surgeon comparison or ranking.
- **Privacy and integration:** Real deployment involves patient health data and varied scheduling systems, so de-identification, access controls and integration effort must be planned before any pilot.

### Success Evidence

- The model shows lower average prediction error than the surgeon-average baseline on held-out test data.
- A higher share of cases is predicted within an agreed tolerance band than with the baseline.
- Under-prediction does not increase compared with the baseline.
- A schedule simulation shows fewer predicted room overruns or less idle time.
- Prototype walkthroughs show that schedulers understand the confidence and override flow.

*Exact go/no-go thresholds will be set in the Data, Model and Evaluation Strategy.*

### Team Recommendation

**Proceed.**

The team recommends proceeding with a narrow MVP for elective case-duration and schedule-risk prediction, embedded in the existing scheduling workflow. The booking decision is repeated daily, the value can be measured against a simple baseline, and the scheduler stays in control. Surgery IQ is positioned as a wider surgical intelligence platform, but this capstone will prove only this first module.
