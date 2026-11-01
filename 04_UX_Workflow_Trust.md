## UX, Workflow and Trust Design - Surgery IQ

**Team 50** | Lead: Deepak Narayanan | Reviewers: Adithya Mohan, Mahender Sivaraman

AI UX is probabilistic, not deterministic. Surgery IQ shows each estimate as a range with a confidence level, and the scheduler always makes the final booking decision.

---

### UX Principle
Surgery IQ should feel like a **quiet second opinion inside the booking screen**, not a separate tool or an autonomous scheduler. It suggests, explains and flags risk. It never books or moves a case on its own.

---

### Main Workflow

**Journey 1 - Scheduler books a case**

| Step | Scheduler action | What Surgery IQ does |
|---|---|---|
| 1 | Opens a case request in the existing scheduling screen | Reads procedure, surgeon, patient and case order inputs |
| 2 | Views the Surgery IQ panel | Shows predicted minutes, likely range, confidence and the surgeon-average baseline |
| 3 | Reviews why | Shows the top 3 factors in plain language |
| 4 | Decides | Accept, adjust or override; adjust or override needs a reason code and a comment |
| 5 | Saves the booking | Recalculates the room-day risk and logs the decision with the comment |

**Journey 2 - Manager reviews the next day's board**

| Step | Manager action | What Surgery IQ does |
|---|---|---|
| 1 | Opens the next-day OR board | Shows each room's booked time against predicted time |
| 2 | Spots at-risk rooms | Flags room-days likely to overrun and lists the main contributing cases |
| 3 | Rebalances if needed | Manager moves or reschedules cases in the existing system; Surgery IQ does not move cases |

---

### Wireframes / Screens

| Screen | What it shows |
|---|---|
| **S1. Case booking panel** | Case details, predicted minutes, likely range, baseline, confidence badge |
| **S2. "Why this estimate" view** | Top 3 factors in plain language, such as "BMI above 35 adds time" |
| **S3. Low-confidence state** | "Needs review" flag, baseline pre-filled, reason for low confidence |
| **S4. Override dialog** | Accept, adjust or override, with a reason code and a comment |
| **S5. Next-day OR board** | Rooms with booked vs predicted time; at-risk room-days flagged |
| **S6. Fallback state** | "Baseline only" label when the model is unavailable or data is missing |

All six screens will be shown in a **single, independent HTML prototype page**, placed in the Appendix with screenshots.

---

### Trust and Explainability

| Question | Our answer |
|---|---|
| **What does the user need to know?** | How long the case is likely to take, how sure the model is, how it compares with the usual estimate, and why it differs |
| **What must be visible?** | Predicted minutes, likely range, confidence level, baseline, top 3 factors, room-day risk, "baseline only" label when in fallback |
| **What should be hidden?** | Raw model scores, model internals, and any comparison or ranking between surgeons |

**Trust features**
- The baseline sits next to every estimate, so the scheduler can see what changed
- Every explanation comes from the model's actual top factors, never invented text
- Confidence is shown with both a word and an icon, so it never depends on colour alone
- The scheduler can see the reason for a low-confidence flag, such as "fewer than 10 past cases"

---

### Uncertainty Handling

| Situation | Behaviour |
|---|---|
| **High confidence behaviour** | Estimate pre-filled; one-click accept; range still shown |
| **Medium confidence behaviour** | Estimate shown with a wider range and factors; scheduler must confirm |
| **Low confidence behaviour** | "Needs review" flag; baseline pre-filled instead of the estimate; scheduler decides |
| **Failure or fallback behaviour** | Model unavailable or data missing: baseline shown with a "baseline only" label; booking never stops |

*Confidence cut-offs will be set in 05_Data_Model_Evaluation.*

---

### Human-in-the-Loop

| Point | Who | What they can do |
|---|---|---|
| Case booking | Scheduler | Accept, adjust or override every estimate |
| Low-confidence cases | Scheduler | Must review before saving; baseline is the default |
| At-risk room-days | Surgical services manager | Decide whether to rebalance; Surgery IQ only flags |
| Override review | Product and data team | Review override comments weekly to find model gaps and improve the model |

**Override for learning**

Every adjust or override captures a reason code and a short comment. The comments are the main learning signal: they show where the model misses real-world factors and feed model review and retraining.

| Reason code | Example comment |
|---|---|
| Surgeon preference | "Surgeon prefers extra time for teaching cases" |
| Known case complexity | "Revision surgery, previous hardware to remove" |
| Equipment or staffing constraint | "Robot shared with OR 5 in the afternoon" |
| Patient-specific factor | "Difficult airway noted in pre-op" |
| Estimate looks wrong | "Range too narrow for this procedure" |
| Other | Free-text comment required |

---
*Surgery IQ is a fictional product created for academic purposes. It uses synthetic data only.*
