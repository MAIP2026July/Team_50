# AI Collaboration Log - Surgery IQ

This log records how the team used AI while doing the product management work. It follows the mandatory packet template and adds a dated entry log starting from the first week of October 2026.

> **Note:** Entries marked `[Team to confirm]` are placeholders. Each member must fill in or delete them based on their actual AI use. Do not submit placeholder rows as real activity.

---

## Tools Used

| Tool                  | Used by  | Main purpose                                                               |
| --------------------- | -------- | -------------------------------------------------------------------------- |
| Microsoft 365 Copilot | Adithya  | Ideation, reviewing the packet, structure mapping, drafting the topic form |
| Claude                | Deepak   | Wireframes and prototype coding                                            |
| Claude                | Mahender | Data generation, model evaluation, economics and risk review               |

## Where AI Helped

| Area        | Status      | How AI helped                                                  |
| ----------- | ----------- | -------------------------------------------------------------- |
| Discovery   | Done        | Generated product idea options and platform-level alternatives |
| Drafting    | Done        | First draft of the Topic Approval Form                         |
| Wireframing | Planned     | Starting layouts for the scheduler screens                     |
| Coding      | Planned     | Prototype scaffolding and model code                           |
| Metrics     | Planned     | Draft evaluation metrics and baseline comparison               |
| Risk review | In progress | Flagged scorecard misuse and the risk of too broad a scope     |

---

## Dated Entry Log

| Week   | Date        | Member            | Tool         | Task                | Prompt summary                                                           | AI output                                                                                                                            | Human decision / correction                                                                                    |
| ------ | ----------- | ----------------- | ------------ | ------------------- | ------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------- |
| Oct W1 | 03 Oct 2026 | Adithya/Mahdender | M365 Copilot | Product ideation    | Suggest AI product ideas that fit the required folder structure          | Six single pain point ideas (implementation delay, chart completion, OR flow, access governance, release risk, roadmap transparency) | Rejected single pain point framing and asked for platform-level ideas                                          |
| Oct W2 | 10 Oct 2026 | Deepak/Mahender   | Claude       | Platform framing    | Suggest platform products with several modules instead of one pain point | Six platform options; recommended "PeriOp IQ"                                                                                        | Chose the surgical platform; renamed it **Surgery IQ** because "PeriOp" is jargon for non-healthcare reviewers |
| Oct W3 | 17 Oct 2026 | Adithya/Deepak    | M365 Copilot | Packet review       | Review the student packet and share thoughts only                        | Flagged that a broad platform matches the "too broad" weak topic pattern; proposed a narrow case duration wedge                      | Accepted the wedge; kept the platform only as the vision                                                       |
| Oct W4 | 24 Oct 2026 | All               |              | Structure mapping   | Compare the faculty folders with the packet structure                    | Found that the prototype and contribution disclosure were missing; proposed adding folders 09 and 10                                 | Kept the faculty structure and added the two folders                                                           |
| Oct W5 | 31 Oct 2026 | All               | Claude       | Role split          | Map the six packet roles to three members                                | Proposed a split: Adithya 01-03, Deepak 04 and 09, Mahender 05-07, shared 08 and 10                                                  | Team to validate in the role discussion                                                                        |
| Oct W5 | 31 Oct 2026 | All               | Claude       | Topic Approval Form | Draft the topic form using the packet template and a peer sample format  | First draft in HTML                                                                                                                  | `[Team to review and edit before submission]`                                                                  |

---

## Example Prompts or Workflows

- **Prompt 1:** "As part of an MBA project, I was told to build a product and need ideas that fit this folder structure. Share ideas, do not create any documents."
- **Prompt 2:** "Do you have ideas for a full product like a surgical analytics platform, rather than taking a single pain point out of the product?"
- **Prompt 3:** "Go through the student packet and present your thoughts. Do not prepare anything."

**Workflow used:** ideas first, then team review, then a decision, then drafting only when explicitly asked.

---

## Where AI Was Weak or Wrong

| Issue               | Example                                                                                     |
| ------------------- | ------------------------------------------------------------------------------------------- |
| Too narrow at first | The first ideas were single features, not products                                          |
| Jargon              | Suggested "PeriOp IQ", a name non-healthcare reviewers may not understand                   |
| Risky scope         | Included surgeon scorecards in the platform modules, which carries bias and misuse risk     |
| Wrong assumption    | Assumed a solo submission based on an earlier course                                        |
| Scope pull          | Platform framing pulled the project toward breadth, while the rubric rewards a narrow wedge |

## Human Corrections

| What we changed                                     | Why                                  | Judgment applied       |
| --------------------------------------------------- | ------------------------------------ | ---------------------- |
| Moved from single features to platform framing      | Wanted a credible product story      | Product strategy       |
| Renamed to Surgery IQ                               | Clarity for a general audience       | Audience awareness     |
| Narrowed the MVP to case duration and schedule risk | The rubric rewards a narrow wedge    | Scope trade-off        |
| Removed surgeon scorecards from the MVP             | Bias and misuse risk                 | Ethics and governance  |
| Synthetic or public data only, fictional brand      | No proprietary data in a public repo | Professional integrity |

---

## Final Reflection

*To be completed at final submission.*

- **Where AI accelerated PM work:** `[Team to complete]`
- **Where AI could not replace PM reasoning:** `[Team to complete]`
