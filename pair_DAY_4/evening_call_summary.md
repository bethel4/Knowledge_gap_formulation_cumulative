# Evening Call Summary

In the evening call, the asker clarified that the explanation needed to produce a concrete implementation plan, not just a general discussion of LLM judge bias. The writer revised the explainer to focus on an order-swapped judging protocol: evaluate A/B, evaluate B/A, map labels back to candidate IDs, and only count wins that remain stable across both orders.

The asker also wanted the recommendation connected more directly to ablation reliability. The revised version now explains that Delta A/B can be inflated if the trained method is consistently placed in the favored position, and recommends reporting unstable-pair rate, position-bias flags, and stable-win-only deltas.

The final revision frames the grounding edit as a change to the judge filter or ablation harness rather than merely a prompt edit.
