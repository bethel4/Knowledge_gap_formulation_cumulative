# Signoff

## Gap Closure

Closed

This explainer fully closed my gap. I now clearly understand the mechanistic reason why templated + style-heavy preference pairs lead to surface optimization, and I have concrete ways to measure and mitigate it.

## What I Understand Now That I Didn’t Before

The model isn’t “cheating” maliciously — it is rationally exploiting the strongest gradient signal in the data. This directly explains why my SimPO judge improved rubric scores but felt shallow on some Tenacious-Bench reasoning slices.

## Grounding Edit Made

I added a new section to `methodology_rationale.md` (and a corresponding ablation in `ablations/`) that decomposes held-out performance into “Style Compliance Score” vs “Decision Reasoning Score” with three new reasoning-only probes. This makes the Week 11 claims much more defensible.
