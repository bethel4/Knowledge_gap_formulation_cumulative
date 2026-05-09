# Question: Day Three

## The Core Question

Because many of our fine-tuning pairs are built from **deterministic style-guide violations** and **templated preferred outputs**, how can we determine whether post-training is improving **genuine decision reasoning** on Tenacious-Bench rather than mainly teaching the model surface-level instruction and style compliance?

## Grounding in the Repo

This question comes directly from how your training data is built.

### Evidence from Code

**In `generation_scripts/build_pairs.py:48`:** Many pairs are formed by taking:
- Preferred output from `ground_truth.preferred_output`
- Rejected output from `candidate_output`

**In `generation_scripts/build_pairs.py:69`:** Trace-derived pairs use a single generic chosen target:

> "Escalate or execute the correct final action with the policy-compliant payment method."

This single target is used for multiple examples.

## The Real Gap

The model may get better at **avoiding obvious stylistic violations** without necessarily getting better at the **deeper reasoning task** your benchmark is supposed to measure, especially:
- Decisive-action quality
- Judgment under constraint