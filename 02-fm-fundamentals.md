---
title: II. FM Fundamentals
nav_order: 3
---

# Part II — Foundation Model Fundamentals
{: .no_toc }

1. TOC
{:toc}

---

## 5. What makes a model a "foundation model"

Three properties, all required:

1. **Pretrained on a broad distribution**, not on the single instance it will be used on.
2. **Transfers** — it is useful on instances it has never seen, zero-shot or with light adaptation.
3. **Serves multiple downstream tasks**, not one.

The contrast that matters here is with a **surrogate**: a surrogate is trained on one system to approximate one model, and it is discarded when that study ends. A foundation model is trained once across many systems and amortised across many studies.

Both are approximation. The difference is entirely in the training distribution and the transfer claim. **This distinction is the whole argument for doing foundation-model work in this domain**, because the existing multi-energy surrogate literature is almost entirely of the first kind.

{: .note }
Property 3 is the one most often quietly dropped. A model that amortises one solve for one task family is a transferable surrogate, not a foundation model. This matters for framing: calling it an FM without multi-task evidence invites exactly the criticism that is hardest to answer.

## 6. The five design decisions

Every foundation model, in any domain, is defined by five choices. Getting these explicit is most of the intellectual work.

### D1 — Unit of observation

What is *one training example*? Language: a token sequence. Vision: a patch grid. Weather: a gridded state at time t.

For energy systems this is genuinely unresolved for planning models, and only obvious for some operational ones. Candidates at system level:

- one timestep of system state
- one (configuration, boundary conditions, trajectory) triple
- one whole model instance
- one modelling decision

{: .note }
Listing candidates is not the same as choosing between them. [Choosing a Basic Element](03-basic-elements.html) supplies a criterion for doing so, and applies it at building level, where the candidates are different and the answer is harder.

### D2 — Tokenisation / encoding

How is a training example turned into something the architecture consumes?

**A useful framing for domain readers:** tokenisation is a discretisation choice. Every simulation begins by deciding what the object is made of — zones, nodes, cells — and that choice fixes what the model can represent, what it must approximate, and how well it carries to a different case. A learned model faces the identical decision. This analogy is the most effective way to explain the problem to a building simulation or energy systems audience, because they have argued about discretisation for decades.

This is where domain-specific difficulty concentrates. Evidence from adjacent fields:

- **Float-heavy data** needs purpose-built handling; work on power-grid foundation models adopts specially designed float tokenisation so that LLMs can process float-rich problems efficiently.
- **Structured codes** break standard schemes: subword tokenisation optimised for natural language fails to capture the hierarchical and compositional structure of structured medical codes, and dedicated tokenisation recovers measurable performance.
- **Multi-domain data** risks structural loss: tokenisation strategies that combine incompatible spatial discretisations risk losing physical adjacency and introducing aliasing effects in attention layers.
- **Multi-resolution data** needs explicit handling: Moirai pairs a multi-patch-size projection scheme handling minute-to-year-scale data with an any-variate attention mechanism that scales to arbitrary numbers of variables.

### D3 — Architecture

Transformer, graph neural network, neural operator, state-space model, or hybrid. Determined largely by what structure the data has (sequence? graph? function?).

### D4 — Pretraining objective

Next-step prediction, masked reconstruction, supervised imitation of a solver, or self-supervised contrastive. For simulation surrogates this is usually supervised regression on solver output; for sequence models, next-token or next-patch prediction.

### D5 — Evaluation

What counts as success, and on what held-out distribution? For physical systems this must include **feasibility and conservation**, not only error.

---
[← Previous: The Domain](01-the-domain.html) · [Next: Choosing a Basic Element →](03-basic-elements.html)
