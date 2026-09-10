---
title: III. Screening Tasks
nav_order: 6
status: draft
last_reviewed: 2026-09-10
---

# Part III — Which Fields Could Support a Foundation Model
{: .no_toc }

{% include page-status.html %}

1. TOC
{:toc}

---

## 8. Screening criteria

A task is a plausible foundation-model target if it scores well on all five. These are the questions to ask before committing.

| # | Criterion | Test |
| :--- | :--- | :--- |
| S1 | **Ground-truth generatability** | Can I produce unlimited correct labels? (Usually: is there a simulator?) |
| S2 | **Task homogeneity** | Do instances share enough structure that transfer is plausible? |
| S3 | **Transfer value** | Are there many instances, such that training once and reusing pays back? |
| S4 | **Bottleneck worth solving** | Is the existing method actually too slow or too costly, *in the loop where it is used*? |
| S5 | **Evaluability** | Is there an objective, checkable success criterion? |

{: .important }
These five screen the **task**. They do not screen the **representation**, and a task can pass all five while remaining unviable because no basic element satisfies the criterion in [§6.6](03-basic-elements.html#66-the-criterion). Run both screens; they are independent.

## 9. Screening the tasks

| Task | S1 ground truth | S2 homogeneity | S3 transfer | S4 bottleneck | S5 evaluable | Verdict |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| T1 UBEM demand | ✔ simulator | ◐ archetype-dependent | ✔ many buildings | ◐ | ✔ | **Good** — but crowded, and representation-limited |
| T2 Resource | ✔ | ✔ | ✔ | ✘ already fast | ✔ | Weak — no bottleneck |
| T3 Forecasting | ✔ observed | ✔ | ✔ | ◐ | ✔ | **Solved** — mature FMs exist |
| **T4 Dispatch** | ✔ solver | ✔ strong | ✔ strong | ✔ in loops | ✔ energy balance | **Strongest candidate** |
| **T5 Design/sizing** | ✔ solver | ◐ | ✔ | ✔ severe | ✔ optimality gap | **Strong, harder** |
| T6 Network sim | ✔ | ◐ topology-specific | ✔ | ✔ | ✔ | **Good** — neural-operator territory |
| T7 Control | ◐ | ◐ | ✔ | ✔ real-time | ◐ | Moderate — RL territory |
| T8 Scenario/pathway | ✘ no ground truth | ✘ | ✔ | ✔ | ✘ | **Weak** — representation problem lives here instead |
| T9 Impact assessment | ✔ | ✔ | ◐ | ✘ | ✔ | Weak — no bottleneck |

## 10. Reading the screen

**T4 (dispatch) is the strongest candidate** and by some distance. It has a simulator (unlimited ground truth), strong structural homogeneity across instances, enormous transfer value, a genuine bottleneck when embedded in loops, and an objective feasibility criterion in the form of energy balance.

**T5 (design) is the highest-value target but harder** — it inherits dispatch as an inner problem, so it is naturally approached *through* T4.

**T1 (UBEM demand) passes the task screen but is crowded and representation-limited.** Novelty here cannot rest on being first to build a surrogate — the metamodel literature is large. It has to rest on the representation question of [§6.7](03-basic-elements.html#67-basic-elements-for-buildings), which is genuinely open and which the existing literature has never treated as a question at all.

**T8 (scenario/pathway) fails the screen for foundation-model treatment**, and this is worth stating plainly because it is where much of the intellectual interest in the domain sits. There is no ground truth (scenarios describe futures that have not occurred), instances are heterogeneous, and success is not objectively checkable. **A scenario is defensible, not correct.** The productive research problem in T8 is not a foundation model — it is *representation*: making the assumptions inside scenarios explicit, comparable and machine-processable. That is a different project with a different method, and conflating the two is a common and costly error.

---
[← Previous: The FM Landscape](04-fm-landscape.html) · [Next: Tier 1 — Single Hub Dispatch →](06-methods-tier1.html)
