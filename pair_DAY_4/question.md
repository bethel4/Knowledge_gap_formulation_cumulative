# The Question

How can we implement position bias mitigation in our judge system, such as by modifying the judge prompt to evaluate pairs in both orders (A-first and B-first) and only count wins that hold across both evaluations?

## Grounded Rationale

From checking the repo, self-preference and length biases are mitigated (different models asserted, content-based rubrics), but position bias is missing—the judge_filter_prompt.md lacks order-swapping or averaging. The text describes position bias as judges favoring the first answer, even on identical content, and fixes it by running evaluations twice with swapped labels, only accepting wins that persist. Implementing this would prevent inflated Delta A scores from artifacts, ensuring reliable ablation results.