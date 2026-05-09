# Morning Call Summary

During the morning call, we clarified that the original question was not simply asking whether LLM judges can be biased, but how to implement a concrete mitigation for **position bias** in the existing judge pipeline. The ambiguous part was whether the fix belonged only in the prompt text or in the evaluation harness itself; we agreed that the real change should be a paired-order evaluation procedure that runs the judge twice, once with candidate A first and once with candidate B first.

We also clarified that the repo already addresses some judge risks, such as avoiding same-model generation and judging, duplicate detection, and content-based quality dimensions. The missing piece is order stability: a candidate should not be counted as a winner unless it wins both when shown first and when shown second.

The sharpened question is therefore about adding a reproducible order-swap protocol to the judge filter and ablation workflow so Delta A/B results are not inflated by presentation artifacts.
