---
title: "4.7 Reading the Screen"
parent: Part 4 — Directions for FMs in UES
nav_order: 7
status: draft
last_reviewed: 2026-09-11
---

# 4.7 Reading the Screen
{: .no_toc }

{% include page-status.html %}

1. TOC
{:toc}

---

**T4 (dispatch) is the strongest candidate** and by some distance. It has a simulator (unlimited ground truth), strong structural homogeneity across instances, enormous transfer value, a genuine bottleneck when embedded in loops, and an objective feasibility criterion in the form of energy balance. See [§4.9.1 (Tier 1)](4-9-1-methods-tier1.html) and [§4.9.2 (Tier 2)](4-9-2-methods-tier2.html) for the build paths.

**T5 (design) is the highest-value target but harder** — it inherits dispatch as an inner problem, so it is naturally approached *through* T4. See [§4.9.3 (Tier 3)](4-9-3-methods-tier3.html).

**T1 (UBEM demand) passes the task screen but is crowded and representation-limited.** Novelty here cannot rest on being first to build a surrogate — the metamodel literature is large. It has to rest on the representation question of [§2.3.2](../part-2-fm-foundations/2-3-choosing-a-basic-element.html#232-basic-elements-for-buildings), which is genuinely open and which the existing literature has never treated as a question at all.

**T8 (scenario/pathway) fails the screen for foundation-model treatment**, and this is worth stating plainly because it is where much of the intellectual interest in the domain sits. There is no ground truth (scenarios describe futures that have not occurred), instances are heterogeneous, and success is not objectively checkable. **A scenario is defensible, not correct.** The productive research problem in T8 is not a foundation model — it is *representation*: making the assumptions inside scenarios explicit, comparable and machine-processable (see [gap G6](../part-6-outlook/6-1-open-gaps.html#g6)). That is a different project with a different method, and conflating the two is a common and costly error.

---
[← Previous: 4.6 Screening the Tasks](4-6-screening-tasks.html) · [Next: 4.8 Candidate Sub-Fields for a New FM →](4-8-candidate-subfields.html)
