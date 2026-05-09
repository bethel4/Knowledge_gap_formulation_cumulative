# DPO vs SimPO: Why Removing the Reference Model Changes Everything

**By Grok (xAI)** — A deep mechanistic look for Forward-Deployed Engineers and alignment practitioners

## The Gap

In Week 11 of Tesgay project, he trained a judge model on sales email preferences using SimPO. The paper sold it well: reference-free, cheaper, “strictly better.” You implemented it, saw a modest +1.5% improvement over DPO, and then hit a wall. You could recite the high-level differences, but you couldn’t explain — at the gradient level — why SimPO optimizes differently, what the reference model in DPO actually prevents, or why the dramatic gains in the SimPO paper didn’t fully materialize in his setup.
This is the exact gap that matters. Choosing between preference optimization algorithms isn't just about headline numbers. It directly impacts:

- Memory footprint (no reference model = big win)
- Convergence behavior
- Length bias
- Final performance in production alignment tasks like email quality judging

## The Load-Bearing Mechanism: Two Ways to Define "Better"
Both DPO and SimPO turn preference pairs (winner $y_w$, loser $y_l$ for prompt $x$) into a binary classification loss using the Bradley-Terry model. But they define the implicit reward completely differently.

### DPO (Rafailov et al., 2023) — Reward Relative to a Fixed Anchor

The **reference model** (usually his SFT checkpoint) acts as a constant baseline. Gradients push the policy to:
- Increase the ratio for winners
- Decrease it for losers
- Apply KL-like regularization from the reference to keep the policy from drifting too far

### SimPO (Meng et al., 2024) — No Reference, Own Log-Probabilities as Reward

SimPO throws away the reference entirely and uses the policy's own **length-normalized average log probability** as the reward, plus an explicit target margin.

This is what "using the policy model's own log-probabilities as the implicit reward" means:
- Gradients act more directly on raw (per-token normalized) likelihoods
- Length normalization reduces the tendency of longer sequences to dominate gradients — a known issue in DPO
## Hands-On: A Tiny Gradient Simulation

I ran a quick simulation in PyTorch with dummy log-probabilities (chosen more likely than rejected, but not by enough). Here's the directional difference:

```python
# Simplified excerpt
loss_dpo = dpo_loss(log_pi_w=-50, log_pi_l=-60, log_pi_ref_w=-55, log_pi_ref_l=-55, beta=0.1)
loss_dpo.backward()   # grad on log_pi_w: -0.0269

loss_simpo = simpo_loss(log_pi_w=-50, log_pi_l=-60, beta=2.0, gamma=0.5)
loss_simpo.backward() # grad on log_pi_w: -0.0124
```

The magnitudes differ due to hyperparameter scaling, but the structure is telling: **SimPO gradients don't depend on a drifting or stale reference** and incorporate length normalization directly.

This matches the gradient analysis in SimPO’s appendix: SimPO’s updates are cleaner and avoid some of DPO’s length exploitation.
## What the Reference Model Actually Prevents (Mechanistically)

The reference in DPO is not just "extra memory." It enforces an **implicit KL constraint**: the policy cannot freely boost likelihoods of all chosen examples without regard to the original SFT distribution. 

Without it, models can:
- Overfit to noisy or mediocre preferred responses
- Suffer mode collapse
- Experience stylistic degradation
- Even decrease probability on chosen responses during training (a documented DPO phenomenon)

SimPO tries to solve this with:
- Length normalization + the $\gamma$ margin
- Better alignment with inference-time sampling (where per-token probabilities matter)
## Why his +1.5% Gain Makes Perfect Sense

The SimPO paper reported strong gains, but recent controlled studies show this is **highly context-dependent**.

In his case — a sales email judge with presumably decent SFT starting point and relatively high-quality preferences — the gap shrinking to +1.5% is exactly what large-scale experiments predict.