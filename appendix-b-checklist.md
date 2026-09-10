---
title: Appendix B — Pre-Project Checklist
nav_order: 13
status: draft
last_reviewed: 2026-09-10
---

# Appendix B — Questions to Ask Before Starting Any Project in This Space

{% include page-status.html %}

1. What is one training example? (D1)
2. **What is the basic element, and does it satisfy all four requirements of [§6.6](03-basic-elements.html#66-the-criterion)?** If not, which one does it break, and what does that cost?
3. Where does ground truth come from, and how much can I generate?
4. What is the loop where the existing method is actually too slow?
5. What am I claiming to generalise over — and does my held-out split test exactly that?
6. **What does a representation-free baseline score, and did I run it before committing to an architecture?**
7. What physical constraints must hold, and by which mechanism ([§15](09-building-it.html#15-enforcing-physics))?
8. What is the honest speedup, including data generation and correction?
9. What are the baselines, and have I included a domain heuristic?
10. Which rare regimes matter, and how am I guaranteeing coverage?
11. **Is this genuinely multi-task, or is it a transferable surrogate being called a foundation model?**
12. What survives if the trained model is thrown away? (Usually: the dataset, the benchmark, the representation.)
13. Has someone already done this in power systems? *(Frequently, yes — check first.)*

---
[← Previous: Glossary](appendix-a-glossary.html) · [Next: Project Notes →](appendix-c-buildfm-bs2027.html)
