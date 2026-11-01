## Product Strategy - Surgery IQ

**Team 50** | Lead: Adithya Mohan | Reviewers: Deepak Narayanan, Mahender Sivaraman

---

### Positioning Statement
For OR schedulers who book elective cases, Surgery IQ is an embedded intelligence module that predicts case duration and schedule risk at the moment of booking. Unlike surgeon averages or dashboards, it gives a per-case estimate with confidence and keeps the scheduler in control.

---

### Product Vision
Every OR day is planned on realistic case estimates, so surgical teams start on time, rooms are not left idle and patients are not cancelled on the day. Surgery IQ delivers this as an intelligence layer inside the scheduling tools hospitals already use.

---

### JTBD

**Primary - OR scheduler**
When I am booking upcoming elective cases into OR blocks, I want a realistic duration for each case and an early warning on rooms likely to overrun, so that I can build a schedule that holds, avoid overtime and cancellations, and still keep control of the final booking.

**Secondary - Surgical services manager**
When I review the next day's OR board, I want to see which rooms are at risk and why, so that I can rebalance cases before the day starts.

---

### Opportunity Framing

**Why this problem matters**

| Impact area | What happens today |
|---|---|
| Cost | Overruns create staff overtime; underruns leave expensive OR time idle |
| Throughput | Late-running rooms push back later cases and can cause same-day cancellations |
| Patient experience | Cancelled or delayed surgery affects timely access to care |
| Frequency | The booking decision is made for every case, every day |

**Why current alternatives are weak**

| Alternative | Weakness |
|---|---|
| Surgeon-requested time | Depends on individual judgment and varies between surgeons |
| Surgeon or procedure average | One number per surgeon and procedure; ignores patient and case factors |
| Fixed buffer rules | Over-books simple cases and under-books complex ones |
| Retrospective dashboards | Explain past overruns but do not estimate upcoming cases |
| Standalone scheduling tools | Hospitals already schedule in existing systems; a new tool adds double entry |

**Why AI may help**
- Combines many case-level factors (procedure, surgeon history, patient profile, case order, anaesthesia type) into one estimate.
- Produces a likely range and a confidence level, not just a single number.
- Rolls case estimates up into a room-day risk that a person cannot easily calculate by hand.
- Learns from actual durations and scheduler overrides over time.

**Why now**
- Surgical scheduling data is already captured digitally in hospital systems.
- Prediction on structured data is cheap to train and run.
- Hospitals are under pressure to make more of existing OR capacity rather than add more rooms.

*These "why now" points are framing assumptions and will be supported with cited sources in the Business, Economics and Scaling section.*

---

### Opportunity Matrix

| Idea | Business Value | Feasibility | Priority |
|---|---|---|---|
| Case duration prediction | High | High | **High - MVP** |
| Room-day overrun risk flag | High | Medium-High | **High - MVP** |
| Confidence routing and override capture | High | High | **High - MVP** |
| Block release recommendation | High | Medium | Phase 2 |
| Turnover time prediction | Medium | Medium | Phase 2 |
| Natural language Q&A on OR performance (GenAI) | Medium | Medium | Later |
| Supply cost per case insights | Medium | Low | Later |
| Surgeon performance scorecards | Medium | Medium | **Excluded** - bias and misuse risk |

---

### RICE Check for MVP Candidates

*Relative team estimates for capstone scope, not measured values. Reach on a 1 to 5 scale, Impact on a 1 to 3 scale, Effort in team-weeks. Confidence scores reflect the team review on 01 Nov 2026.*

| Feature | Reach | Impact | Confidence | Effort | RICE score |
|---|---|---|---|---|---|
| Room-day overrun risk flag | 4 | 3 | 80% | 2 | 4.8 |
| Case duration prediction | 5 | 3 | 90% | 3 | 4.5 |
| Confidence routing and override | 5 | 2 | 90% | 2 | 4.5 |
| Block release recommendation | 3 | 3 | 70% | 4 | 1.6 |
| GenAI Q&A | 3 | 1 | 50% | 3 | 0.5 |

**Reading:** The top three score close together and depend on each other, since the risk flag needs the duration estimate and routing needs its confidence. They are built together as one MVP. Block release stays clearly below the MVP group and moves to Phase 2. GenAI Q&A waits for a later phase.

---

### Platform vs Feature

**Decision:** Start as an embedded feature, grow into a platform.

| Stage | What Surgery IQ is | What it reuses |
|---|---|---|
| MVP | Case-duration and schedule-risk module inside the existing scheduling screen | - |
| Phase 2 | Adds block release and turnover prediction | Same data feed, integration and override loop |
| Phase 3 | Surgical intelligence layer with GenAI Q&A and cost insights | Shared data model and governance controls |

**Course case - Amazon vs ChatGPT (feature vs platform logic)**

| Question | Our answer |
|---|---|
| What is similar? | A product choosing between being a feature inside an existing experience or a standalone destination |
| What is different? | Hospitals rarely replace core scheduling systems, so the standalone route is even harder for us |
| What lesson transfers? | Win adoption inside the existing workflow first, then expand from shared data |
| What would we do differently? | Treat integration as a phase-gated dependency, not a launch requirement, by proving value with a simulated host screen first |

---

### Build vs Buy vs Partner/API

- **Recommended path:** Build the prediction module; use an LLM API only for optional plain-language explanations; partner for scheduling system integration.
- **Why:**
  - Duration prediction is a structured data problem that a lightweight model handles well and cheaply.
  - The value sits in the workflow (estimate at booking, confidence routing, override loop), which we need to own.
  - Hospitals will not replace their scheduling systems, so integration is best done through partners and standard interfaces.
  - Buying an existing OR analytics product would not let us control the confidence and override design.
- **Main trade-offs:**

| Choice | Gain | Cost |
|---|---|---|
| Build the model | Control, low running cost, explainable | Needs local data and periodic retraining |
| API for explanations | Fast to add readable text | Per-call cost; must be limited to real model drivers to avoid invented reasons |
| Partner for integration | No need to build scheduling basics | Dependency on partners; integration differs by hospital |

---

### First Wedge

| Element | Scope |
|---|---|
| Setting | One fictional mid-size hospital, 6 to 8 ORs |
| Case type | Elective, scheduled cases only |
| Specialties | Orthopaedics, general surgery, urology (proposed) |
| Users | OR schedulers (primary), surgical services manager (secondary) |
| Moment of use | When a case is booked and when the next day's board is reviewed |
| Data | Synthetic data only, clearly labelled |
| **Out of scope** | Emergency cases, auto-booking, block reallocation, surgeon comparisons or rankings |

**Course case - Swiggy (ETA prediction)**

| Question | Our answer |
|---|---|
| What is similar? | A repeated time estimate where accuracy and visible confidence drive user trust |
| What is different? | Errors affect patient care and staff, not just delivery delays, so human control matters more |
| What lesson transfers? | Keep AI largely invisible inside the workflow and judge it on how well its estimates hold up |
| What would we do differently? | Show the range and confidence openly and let the scheduler override, rather than presenting one silent number |

---

### Key Strategic Choices

| Choice | Option rejected | Reason |
|---|---|---|
| Embedded module | Standalone planner | Fits existing workflow; easier to adopt and sell |
| Narrow wedge | Broad surgical platform from day one | Rubric rewards a provable MVP |
| Human decides | Auto-booking | Under-prediction risk to patients and staff |
| No surgeon scorecards | Surgeon comparison in MVP | Bias and misuse risk |
| Synthetic data | Real or proprietary data | Privacy and academic integrity |

---
*Surgery IQ is a fictional product created for academic purposes. It uses synthetic data only.*
