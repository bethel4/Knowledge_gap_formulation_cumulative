# Day 3 Morning Call — Bethel Pair Session
## Participants
- Tsegay
- Bethel
## Date
- 2026-07-07

## Duration
- ~25 minutes
## Session Goal
Align on today’s topic (**Training and post-training mechanics**), exchange draft questions, and finalize one sharp question each for the explainer round.

## What We Covered
1. We connected on time and started with a brief alignment on the expectations for Day 3.
2.  We decided to concentrate on the underlying mechanisms rather than high-level or surface definitions.
3. We reviewed our draft questions together, examining them line by line to ensure:
-   strong diagnostic clarity,
-   grounding in concrete artifacts,
-   applicability beyond a single repository,
    and the ability to be fully addressed within one explainer.




## Bethel’s Question (Finalized)
Because many of our fine-tuning pairs are built from deterministic style-guide violations and
  templated preferred outputs, how can we determine whether post-training is improving genuine
  decision reasoning on Tenacious-Bench rather than mainly teaching the model surface-level
  instruction and style compliance?

## Grounding in the repo

  This question comes directly from how your training data is built.

  In generation_scripts/build_pairs.py:48, many pairs are formed by taking a preferred output from
  ground_truth.preferred_output and a rejected output from candidate_output. In the same file,
  trace-derived pairs use a single generic chosen target, "Escalate or execute the correct final
  action with the policy-compliant payment method.", for multiple examples in generation_scripts/
  build_pairs.py:69.
 So the real gap is:
  the model may get better at avoiding obvious stylistic violations without necessarily getting
  better at the deeper reasoning task your benchmark is supposed to measure, especially decisive-
  action quality and judgment under constraint.
## Tsegay's Question(Finalized)
In my Week 11 project, I trained a SimPO judge to evaluate sales emails. I chose SimPO over DPO because the SimPO paper claimed it's "reference-free" and cheaper. But after reading both papers, I realized I cannot explain the actual gradient difference between DPO and SimPO.
My specific gap: I understand that DPO uses a reference model (typically the SFT model) to compute a reward margin, while SimPO eliminates that reference model entirely. But I cannot explain:

What SimPO actually optimizes: The paper says SimPO uses the policy model's own log-probabilities as the implicit reward. What does this mean at the gradient level? How does the loss landscape differ from DPO?
The trade-off: Under what conditions would DPO still outperform SimPO? The paper claims SimPO is strictly better, but my own results show only a +1.5% improvement - not the dramatic gap they reported. What factor might explain this?
The reference model's role: When DPO uses an SFT reference model, what is it actually preventing? The paper says "overfitting to the preference data" - but what does that mean mechanistically?
Grounded in: My Week 11 methodology_rationale.md (SimPO justification) and training/run_simpo.py lines 80-100 (loss function implementation).
Why this matters: Every FDE choosing a preference tuning algorithm needs to understand the actual gradient difference, not just which paper had a better headline number. The choice between DPO and SimPO affects memory footprint, convergence speed, and final performance.
What a good answer looks like:

Explains the loss function difference with actual equations
Shows a small simulated experiment comparing gradients
Cites the original DPO paper (Rafailov et al., 2023) and SimPO paper (Meng et al., 2024)
Gives a decision rule for choosing between them
## My Takeaways From the Morning Call

1. **Both questions are mechanistically grounded** — Neither is asking for high-level intuition. Bethel's is about separating signal (reasoning) from noise (style compliance) in training data. Tsegay's is about understanding gradient-level differences between DPO and SimPO. Both require precision.

2. **The reference model problem is central to both** — Bethel's question hinges on what signal we're optimizing for. Tsegay's hinges on what the reference model prevents. These might converge: if SimPO lacks a reference anchor, does it risk mode collapse into stylistic overfitting (Bethel's concern)?

3. **Empirical results should drive the explainer, not the paper claims** — Tsegay's +1.5% result vs. SimPO's claimed dramatic gains is the real data point. An effective explainer needs to explain *why* the gap narrows in practice, not just retell the paper's theoretical story.

4. **Action items are complementary** — Tsegay writes the mechanics explainer (gradient-level, equations, decision rules). Bethel reviews for clarity and reproducibility. Then we can test whether understanding DPO vs. SimPO mechanics helps Bethel's question about training signal purity.

5. **Success metric is clear** — A good explainer answers: What does SimPO optimize at the gradient level? What does a reference model prevent? Under what conditions does DPO still win? And: how should this inform the choice between algorithms?

## Action Items Before Evening Call

- Tsegay: write explainer focused on strategy mechanics + cost equations + implementation edits.
- Bethel: review and prepare feedback on clarity, reproducibility, and recommendation strength.

