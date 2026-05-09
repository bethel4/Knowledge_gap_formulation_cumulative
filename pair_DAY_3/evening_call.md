# Day 3 Evening Call — Bethel Pair Session

## Participants
- Tsegey
- Bethel

## Date
- 2026-05-07

## Duration
- ~35 minutes
## Session Goal
Exchange explainers, stress-test whether each explainer actually closes the paired question, and record concrete revision decisions.
## What We Did

1. We exchanged explainers before the call and read each other’s drafts in advance.
2. During the call, we reviewed each explainer against the rubric dimensions:
   - gap closure,
   - mechanism naming,
   - source quality,
   - hands-on demonstration,
   - scope discipline,
   - public-artifact readiness.
3. We discussed where each draft was strong and where language needed tightening.
## Discussion on Tsegay’s Explainer

Tsegay walked through the "DPO vs SimPO" draft. Bethel read it carefully and flagged a critical issue: **authorship consistency**.

### The Authorship Problem

The explainer switches voice multiple times:
- Opens with "A peer of mine trained a model" (observer voice)
- Then shifts to "I chose SimPO" (first-person implementer)
- Then "I ran a tiny PyTorch gradient comparison" (experimenter voice)
- Then "We tested this" (collaborative voice)

**Result:** Readers can't tell if this is Tsegay's lived experience, a research synthesis, or a collaborative writeup.

### Decision Made

We agreed on **consistent authorship:** Since Tsegay is the primary person who:
- Led the Week 11 project
- Made the SimPO choice
- Implemented the training
- Observed the +1.5% result

…the explainer should use **"I/my" throughout** to own the experience.

This means:
- "I chose SimPO" (keep as-is, own the choice)
- "my setup" instead of "the project setup"
- "I ran a small gradient simulation to test this" instead of "A simulation made the distinction clearer"
- Remove generic "we" observations; keep collaborative insights in the call notes instead

### Secondary Fix: The Gradient Simulation

The line "I ran a tiny PyTorch gradient comparison" needs a quick check: **Did you actually code and run this, or is this a conceptual illustration?**

If actual code ran: keep it, own it.
If conceptual: reword to "A small gradient simulation shows why..." and clarify in a footnote that this illustrates the mechanism.

## Revision Notes Agreed

1. **Authorship pass:** Convert to consistent first-person. Tsegay owns the voice and experience throughout.
2. **Gradient simulation:** Clarify whether empirical or illustrative. Cite accordingly.
3. **Reference model section:** The explanation of what KL constraint prevents is strong. Keep as-is.
4. **Context for readers:** Add a brief intro line like: "This post explains the gradient-level difference that shaped my choice between DPO and SimPO in practice."
5. **Scope check:** Confirmed the explainer stays focused on mechanistic gap closure, doesn't drift into broader preference tuning philosophy.

## Outcome

- Tsegay's explainer is **mechanically sound and well-sourced**.
- After authorship consistency pass, it will be **ready for external sharing**.
- Bethel will review the revised draft for final tone and flow before signoff.
- The pairing successfully closed both knowledge gaps: Bethel's (signal purity in training data) and Tsegay's (gradient-level DPO vs SimPO mechanics).

## Final Takeaways

1. **Authorship clarity matters as much as technical accuracy** — Readers need to know whether you're reporting lived experience, citing research, or synthesizing both. Mixing voices breaks trust.
2. **The DPO vs SimPO choice is a proxy for deeper questions** — Understanding the reference model's role in regularization opens up better judgment across many alignment scenarios, not just this one.
3. **Empirical results trump paper claims** — Tsegay's +1.5% vs. the paper's dramatic gap is the real signal. A good explainer explains why that gap narrows, not why the headline failed.
4. **Both explainers strengthen each other** — Understanding DPO's reference model (Tsegay) gives context for Bethel's question about training signal purity. Both are versions of the same core problem: how to know what your model is actually learning.

## Next Actions

- Tsegay: 
  - Revise "DPO vs SimPO" draft with consistent first-person authorship.
  - Clarify gradient simulation section (empirical or illustrative?).
  - Add opening context line about why this gap mattered to the Week 11 project.
  - Submit revised draft for Bethel's final tone review by EOD.

- Bethel: 
  - Review Tsegay's revised explainer for voice consistency and readability.
  - Finalize own signoff document (question closure confirmation, public readiness assessment).
  - Prepare pair-day artifact summary for Bethel's feedback loop (if applicable).

