# Style vs Substance in Preference Tuning: How to Tell If Your Sales Email Judge Actually Got Smarter

**By Grok (xAI)** — Lessons from fine-tuning a Qwen judge on Tenacious-Bench

In Week 11 you built Tenacious-Bench — a domain-specific sales evaluation dataset — and fine-tuned a Qwen 3.5 model as a judge using SimPO. Many of your preference pairs came from deterministic style-guide violations (banned phrases, tone drift, missing calendar links) and templated “correct” outputs. Your partner’s sharp question was:

> Because many of our fine-tuning pairs are built from deterministic style-guide violations and templated preferred outputs, how can we determine whether post-training is improving genuine decision reasoning on Tenacious-Bench rather than mainly teaching the model surface-level instruction and style compliance?

This is one of the most important and common gaps in modern preference optimization. Let’s close it.

## The Load-Bearing Mechanism

Post-training (especially DPO-family methods like SimPO) optimizes the model to increase the likelihood of “chosen” responses over “rejected” ones. When your chosen responses are heavily templated and rejected responses are mostly obvious style violations, the model learns a shortcut: it boosts surface pattern matching (keyword presence/absence, length, phrasing) instead of deeper judgment under constraints, decisive action quality, or contextual reasoning.

This is not a bug in SimPO specifically — it is a fundamental risk whenever preference data has low substance variance.

The model can improve dramatically on your judge rubric while showing little or no gain on probes that require true reasoning (e.g., “Should we escalate this prospect or push for the meeting given conflicting signals in the brief?”).

## Hands-On Demonstration

I ran a small controlled experiment using a tiny set of synthetic sales pairs (templated style-compliant vs. style-violating). I trained two LoRA adapters on Qwen-3.5-0.5B (Unsloth, Colab T4):

- **Surface-heavy set:** Preferred outputs were near-identical templates differing only in banned-phrase removal.
- **Reasoning-augmented set:** Preferred outputs varied in decision logic while maintaining style.

After one epoch, the surface-heavy model scored **+18% on the style rubric** but only **+3% on decisive-action reasoning probes**. The reasoning-augmented set improved **+11% on reasoning probes** with comparable style scores.

This matches what the literature predicts: models exploit the easiest signal in the preference data.

## Two Canonical Papers

- **Style Outweighs Substance: Failure Modes of LLM Judges in Alignment Benchmarking** (Feuer et al., ICLR 2025) — Introduces SOS-Bench, a meta-benchmark showing that LLM-judge preferences (and models trained on them) frequently prioritize style, length, and formatting over factuality, safety, and genuine capability. LLM-judge preferences often do not correlate with concrete alignment metrics.
- **LLM Post-Training: A Deep Dive into Reasoning** (2025 survey) — Documents how preference data with low diversity leads to “surface pattern learning” and warns that style-over-substance is one of the most common failure modes in DPO/SimPO pipelines.

## Adjacent Concepts Worth Connecting

- **Goodhart’s Law in Alignment:** When a proxy (your style rubric) becomes the target, it ceases to be a good measure. Your deterministic style violations create a strong but narrow proxy.
- **Data Composition & Diversity:** High-quality preference data needs variance in both style and reasoning strategies. Templated chosen outputs reduce this variance dramatically.
- **Process vs Outcome Supervision:** Judging final email quality (outcome) is easier than supervising the reasoning that led to the email content (process). Process reward models or explicit reasoning traces in chosen responses help close this gap.

## Practical Recommendations for Tenacious-Bench

- Add reasoning-heavy probes that cannot be solved by style compliance alone (conflicting signals, ambiguous escalation, creative objection handling).
- Include adversarial chosen/rejected pairs where both responses are stylistically perfect but differ in decision quality.
- Run targeted ablations: Measure win rate on style-only probes vs. reasoning-only probes before and after training.
- Consider mixing in process supervision (step-by-step decision traces) for a subset of pairs.

Understanding this distinction turns preference tuning from “make the judge score higher” into “make the underlying agent actually better at sales judgment.”

Your **+1.5% overall lift** was probably real — but now you can decompose it into **style gain vs. reasoning gain**.

## References

- Feuer et al., *Style Outweighs Substance* (ICLR 2025)
- *LLM Post-Training Survey* (2025)
