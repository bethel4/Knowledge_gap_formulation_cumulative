# Canonical List for Forward-Deployed Engineers

This list is built only from source files in `pair_DAY_1` through `pair_DAY_4`. Links are included only when they appeared in the repo. Entries with incomplete or uncertain metadata are placed under `Needs Verification`.

## Papers

### Efficient Memory Management for Large Language Model Serving with PagedAttention

- **Authors:** Woosuk Kwon, Zhuohan Li, Siyuan Zhuang, Ying Sheng, Lianmin Zheng, Cody Hao Yu, Joseph E. Gonzalez, Hao Zhang, Ion Stoica
- **Link:** https://doi.org/10.1145/3600006.3613165; https://arxiv.org/pdf/2309.06180
- **Where it appeared in my repo:** `pair_DAY_1/sources.md`
- **Why it matters:** This is the primary source for KV-cache memory management and the serving-layer mechanics behind high-throughput LLM inference.
- **Key takeaway for FDEs:** Inference cost and latency are not just model-size problems. KV-cache growth, fragmentation, and sequence length directly shape throughput and cost.

### Towards Green AI: Decoding the Energy of LLM Inference in Software Development

- **Authors:** Lola Solovyeva, Fernando Castor
- **Link:** https://arxiv.org/abs/2602.05712
- **Where it appeared in my repo:** `pair_DAY_1/sources.md`
- **Why it matters:** The Day 1 explainer used this paper to separate prefill and decode energy/cost and to reason about output-token verbosity.
- **Key takeaway for FDEs:** Optimize what dominates the bill. Reducing unnecessary generated tokens can matter more than only shortening prompts.

### Which Agent Causes Task Failures and When? On Automated Failure Attribution of LLM Multi-Agent Systems

- **Authors:** Zhang et al.
- **Link:** Not provided in repo
- **Where it appeared in my repo:** `pair_DAY_2/source.md`, `pair_DAY_4/source.md`
- **Why it matters:** It formalizes failure attribution as identifying both the responsible agent/component and the failure step.
- **Key takeaway for FDEs:** Multi-step agent failures should be logged as `(component, step, reason)`, not collapsed into a single final success/failure label.

### Judging LLM-as-a-Judge with MT-Bench and Chatbot Arena

- **Authors:** Zheng et al.
- **Link:** Not provided in repo
- **Where it appeared in my repo:** `pair_DAY_4/source.md`
- **Why it matters:** The source file identifies this as the reference for LLM-judge limitations such as position bias, verbosity bias, and self-enhancement bias.
- **Key takeaway for FDEs:** Automated judges need bias controls, including answer-order swapping, before their scores can support product or model claims.

### A Survey on LLM-as-a-Judge

- **Authors:** Gu et al.
- **Link:** Not provided in repo
- **Where it appeared in my repo:** `pair_DAY_2/source.md`, `pair_DAY_4/source.md`
- **Why it matters:** The source files use this survey to ground evaluation reliability problems in automated judging systems.
- **Key takeaway for FDEs:** LLM-as-a-judge can be useful, but only when its biases, calibration limits, and evaluation protocol are explicit.

### Let's Verify Step by Step

- **Authors:** Lightman et al.
- **Link:** Not provided in repo
- **Where it appeared in my repo:** `pair_DAY_2/source.md`
- **Why it matters:** Listed as the process-level supervision reference for step attribution and process reward models.
- **Key takeaway for FDEs:** Evaluating intermediate reasoning or execution steps can expose failures that final-answer evaluation hides.

### DeepSeek-Math

- **Authors:** Shao et al.
- **Link:** Not provided in repo
- **Where it appeared in my repo:** `pair_DAY_2/source.md`
- **Why it matters:** Cited as process reward model work relevant to scoring intermediate steps.
- **Key takeaway for FDEs:** If an agent has multi-step reasoning or tool execution, step-level signals can be more actionable than only final outcomes.

### Datasheets for Datasets

- **Authors:** Gebru et al.
- **Link:** Not provided in repo
- **Where it appeared in my repo:** `pair_DAY_2/source.md`
- **Why it matters:** Used as a dataset documentation standard for failure logs and evaluation datasets.
- **Key takeaway for FDEs:** Logs become datasets once they drive evaluation or training; document their provenance, structure, and limitations.

### Data Cards

- **Authors:** Pushkarna et al.
- **Link:** Not provided in repo
- **Where it appeared in my repo:** `pair_DAY_2/source.md`
- **Why it matters:** Listed as a standard for documenting dataset design and failure taxonomies.
- **Key takeaway for FDEs:** Evaluation artifacts need documentation as much as models do, especially when other engineers will reuse them.

### DPO

- **Authors:** Rafailov et al.
- **Link:** Not provided in repo
- **Where it appeared in my repo:** `pair_DAY_2/source.md`
- **Why it matters:** Cited as preference-learning work relevant to training failure-judging models.
- **Key takeaway for FDEs:** Preference optimization choices affect model behavior, reproducibility, and how much the policy stays anchored to prior behavior.

### SimPO

- **Authors:** Meng et al.
- **Link:** Not provided in repo
- **Where it appeared in my repo:** `pair_DAY_2/source.md`
- **Why it matters:** Cited as preference-learning work relevant to failure judging and preference-trained systems.
- **Key takeaway for FDEs:** Reference-free preference optimization can reduce overhead, but it still requires careful evaluation of what signal the model is learning.

### ORPO

- **Authors:** Hong et al.
- **Link:** Not provided in repo
- **Where it appeared in my repo:** `pair_DAY_2/source.md`
- **Why it matters:** Listed as preference-learning work for judging models.
- **Key takeaway for FDEs:** Alignment methods are not interchangeable implementation details; each changes cost, training dynamics, and failure modes.

### Prometheus 2

- **Authors:** Kim et al.
- **Link:** Not provided in repo
- **Where it appeared in my repo:** `pair_DAY_2/source.md`
- **Why it matters:** Listed as judge-model work for automatically distinguishing good and bad outputs or failure types.
- **Key takeaway for FDEs:** Dedicated judge models can support scalable evaluation, but their protocols and biases still need documentation.

### Style Outweighs Substance: Failure Modes of LLM Judges in Alignment Benchmarking

- **Authors:** Feuer et al.
- **Link:** Not provided in repo
- **Where it appeared in my repo:** `pair_DAY_3/source.md`
- **Why it matters:** Used to ground the Day 3 concern that LLM judges and preference data may reward style, length, or formatting over deeper capability.
- **Key takeaway for FDEs:** If the training or evaluation data contains easy style shortcuts, a model may improve the score without improving the real task.

### LLM Post-Training: A Deep Dive into Reasoning Large Language Models

- **Authors:** Not provided in repo
- **Link:** Not provided in repo
- **Where it appeared in my repo:** `pair_DAY_3/source.md`
- **Why it matters:** Listed as a 2025 survey relevant to reasoning-focused post-training.
- **Key takeaway for FDEs:** Post-training gains should be decomposed by capability slice, not treated as a single aggregate improvement.

### Efficiently Scaling Transformer Inference

- **Authors:** Pope et al.
- **Link:** Not provided in repo
- **Where it appeared in my repo:** `pair_DAY_1/sources.md`
- **Why it matters:** Listed as follow-on reading for the prefill/decode compute distinction.
- **Key takeaway for FDEs:** Serving performance depends on the different compute profiles of prompt processing and token generation.

## Tools and Documentation

### vLLM

- **Link:** https://github.com/vllm-project/vllm
- **Why it matters:** Day 1 identifies vLLM as the open-source LLM serving system built on PagedAttention.
- **Practical use case:** Use it when self-hosting or benchmarking LLM inference where KV-cache memory management and throughput matter.

### FasterTransformer

- **Link:** Not provided in repo
- **Why it matters:** Listed in Day 1 as a baseline system in the PagedAttention evaluation.
- **Practical use case:** Use as a reference point when comparing transformer inference serving approaches.

### Who&When Dataset

- **Link:** Not provided in repo
- **Why it matters:** Mentioned with the automated failure attribution paper as the dataset for evaluating who caused a failure and when.
- **Practical use case:** Use as a conceptual model for designing trace-level failure attribution benchmarks.

### SOS-Bench

- **Link:** Not provided in repo
- **Why it matters:** Mentioned with `Style Outweighs Substance` as a benchmark for style-over-substance failures in LLM judging.
- **Practical use case:** Use as a reference idea when designing eval slices that separate surface compliance from real capability.

## Engineering Patterns

### Structured Tracing

- **What it means:** Every agent step emits a typed record with fields such as `trace_id`, `step`, `component`, `input`, `output`, `status`, `latency_ms`, and `error_type`.
- **Why FDEs should care:** Without structured traces, production failures collapse into vague outcomes that cannot be debugged or evaluated.
- **Supported by:** `pair_DAY_4/source.md`; `Who&When`; Day 4 failure attribution concepts.

### Causal Attribution

- **What it means:** A failure is assigned to the responsible component and step, not just to the overall system.
- **Why FDEs should care:** It lets teams separate model failure, orchestration failure, tool failure, stale state, and runtime failure.
- **Supported by:** `Who&When`; Day 2 and Day 4 source files.

### Reproducible Evaluation

- **What it means:** Evaluation results include the strategy, parameters, trace records, and task-level outcomes needed for another engineer to rerun the result.
- **Why FDEs should care:** A score without selection strategy, candidate count, or trace metadata is hard to trust.
- **Supported by:** Day 2 source themes; LLM-as-a-judge sources; dataset documentation sources.

### pass@k Evaluation

- **What it means:** Measures whether a system solves a task across multiple attempts.
- **Why FDEs should care:** Agent systems often have stochastic attempts; pass@k only becomes meaningful when trials are independent and logged.
- **Supported by:** `pair_DAY_4/source.md`.

### Bootstrap Confidence Intervals

- **What it means:** Estimates uncertainty in benchmark results through resampling task-level outcomes.
- **Why FDEs should care:** It helps avoid overclaiming small benchmark deltas, especially in held-out evals.
- **Supported by:** `pair_DAY_4/source.md`.

### LLM-as-a-Judge Reliability

- **What it means:** Automated judging must account for position bias, verbosity bias, self-enhancement bias, and calibration limitations.
- **Why FDEs should care:** Judge bias can create fake model improvements or inflated ablation results.
- **Supported by:** Zheng et al.; Gu et al.; Day 4 source file.

### Agent Observability

- **What it means:** Agent systems expose enough runtime state to replay and explain decisions, tool calls, errors, and business outcomes.
- **Why FDEs should care:** Observability turns debugging from guesswork into a structured engineering process.
- **Supported by:** `pair_DAY_4/source.md`; Who&When; agent/tooling foundation sources.

### Dataset Documentation

- **What it means:** Training, evaluation, and failure-log datasets include clear documentation of collection method, labels, known limitations, and intended use.
- **Why FDEs should care:** Poorly documented eval data makes benchmark numbers hard to interpret and easy to overfit.
- **Supported by:** Gebru et al.; Pushkarna et al.; Day 2 source file.

### Style-vs-Reasoning Decomposition

- **What it means:** Evaluation separates surface compliance from deeper decision quality or reasoning.
- **Why FDEs should care:** Preference-tuned systems can improve visible style metrics without improving the real business task.
- **Supported by:** Feuer et al.; `LLM Post-Training: A Deep Dive into Reasoning Large Language Models`; Day 3 source file.

### Inference Cost Decomposition

- **What it means:** Separate prefill/input costs from decode/output costs and cache-related serving effects.
- **Why FDEs should care:** Cost reduction should target the real driver, often generated-token volume rather than only prompt length.
- **Supported by:** PagedAttention; Solovyeva and Castor; Pope et al.

## Needs Verification

These entries appeared in source files but did not include enough metadata in the repo to treat as clean canonical citations.

- **Hong et al., 2023 - Multi-agent LLM collaboration frameworks**
  - **Where it appeared:** `pair_DAY_2/source.md`
  - **Missing/uncertain:** Full title, author list, link, venue.

- **Wu et al., 2023 - Agent interaction protocols**
  - **Where it appeared:** `pair_DAY_2/source.md`
  - **Missing/uncertain:** Full title, author list, link, venue.

- **Li et al., 2023 - Tool-augmented LLM systems**
  - **Where it appeared:** `pair_DAY_2/source.md`
  - **Missing/uncertain:** Full title, author list, link, venue.

- **Liu et al., 2024 - Best Practices on Synthetic Data**
  - **Where it appeared:** `pair_DAY_2/source.md`
  - **Missing/uncertain:** Full title, author list, link, venue.

- **Xu et al., 2024 - Magpie (self-generated instruction data)**
  - **Where it appeared:** `pair_DAY_2/source.md`
  - **Missing/uncertain:** Full title, author list, link, venue.

- **Chen et al., 2025 - Dynamic Evaluation & Contamination**
  - **Where it appeared:** `pair_DAY_2/source.md`
  - **Missing/uncertain:** Full title, author list, link, venue.

- **Shinn et al., 2024 - Self-reflection in agents**
  - **Where it appeared:** `pair_DAY_2/source.md`
  - **Missing/uncertain:** Full title, author list, link, venue.

- **Huang et al., 2023 - LLM reasoning failures**
  - **Where it appeared:** `pair_DAY_2/source.md`
  - **Missing/uncertain:** Full title, author list, link, venue.

- **Orca (Yu et al., 2022)**
  - **Where it appeared:** `pair_DAY_1/sources.md`
  - **Missing/uncertain:** Full title, complete author list, link, venue. The repo identifies it only as an iteration-level scheduling system that PagedAttention improves upon.
