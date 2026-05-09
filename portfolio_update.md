# Portfolio Update

## Overview

This week strengthened my Weeks 10-11 portfolio by adding the engineering layer that makes AI systems defensible after they run: attribution, observability, reproducible evaluation, and source-grounded technical communication. Across `pair_DAY_1` through `pair_DAY_4`, I worked from peer questions, explainers, source files, threads, signoffs, and grounding notes to close gaps that were directly tied to production agent work.

The main portfolio improvement is that my work now shows more than model usage or benchmark claims. It shows that I can identify where an AI system is opaque, trace the mechanism causing the problem, connect the explanation to credible sources, and turn that understanding into concrete evaluation or implementation guidance.

## Five Grounding Contributions

1. **Failure attribution for a multi-step Conversion Engine**

   In `pair_DAY_4`, I grounded the strongest contribution in a Week 10-style Conversion Engine path: reply classification, HubSpot lookup/update, Cal.com link generation, LLM reply drafting, and Resend delivery. The core improvement was reframing a generic "booking failed" outcome into step-level attribution: which component failed, at which step, and why. The grounding notes point to typed trace schemas, traced service wrappers, per-turn JSONL trace persistence, classification confidence and alternatives, and a failure-attribution resolver. For an FDE, this is the difference between a demo that works once and a system that can be debugged in the field.

2. **Structured observability instead of raw logs**

   The Day 4 explainer and thread separate logs from traces. A useful trace preserves model-visible state, selected action, tool arguments, tool results, retries, fallback behavior, errors, and business outcome. That design makes failures replayable and attributable across model, orchestration, tool, runtime, and external-state layers. This contribution matters because real customer deployments fail in mixed ways; observability has to support diagnosis, not just record activity.

3. **Reproducible judge-based evaluation**

   In `pair_DAY_2`, I focused on the hidden interface between a trained judge score and the generator's next action. The work clarified rejection sampling, best-of-N, and reranking as distinct inference-time selection strategies with different cost, latency, and reproducibility profiles. The practical outcome was a clear requirement to log `decoding_strategy`, `n_candidates`, `threshold`, and `max_tries` in artifacts such as `scoring_evaluator.py`, `ablation_results.json`, and `model_card.md`. This strengthens my Week 11 portfolio by making benchmark deltas inspectable rather than dependent on an implicit library default.

4. **Benchmark validity for preference tuning**

   In `pair_DAY_3`, I identified a risk in preference data built from deterministic style-guide violations and templated preferred outputs. The technical question was whether post-training improved genuine decision reasoning or mainly taught surface compliance. The grounded answer was to separate style-compliance probes from decision-reasoning probes and add adversarial pairs where both outputs are stylistically acceptable but differ in judgment quality. This contribution shows evaluation maturity: I am not satisfied with an aggregate score unless I know what capability actually improved.

5. **Inference-cost grounding for LLM systems**

   In `pair_DAY_1`, the work decomposed why a constrained prompt setup cost 73% more per task. The explanation separated prefill from decode, connected KV-cache behavior to inference cost, and showed that output verbosity was the dominant driver. My asker-side gap also focused on prefix caching and measurement for repeated system prompts: cache-hit status, token counts, model name, and cost estimates. This matters for FDE work because cost claims become fragile when they are not tied to observable usage data.

## Technical Growth

This week improved my debugging methodology. I got better at finding the exact interface where a system's claim becomes undefended: cache behavior across repeated LLM calls, judge-score coupling, pair-order bias, style leakage in training data, and failure attribution across tool pipelines.

I also improved at turning research into engineering patterns. The papers and source notes around PagedAttention, LLM-as-a-judge reliability, automated failure attribution, process supervision, dataset documentation, and style-over-substance failures became practical design rules: preserve traces, log selection strategy, document evaluation data, separate benchmark slices, and report uncertainty.

## Research and Communication Impact

The week made my technical communication more useful to engineers. Each explainer had to do more than summarize a paper. It had to answer what mechanism matters, what source supports the claim, what repo artifact is affected, and what should change next.

The public posts and threads also show that I can compress technical work without losing the operational point. That is important for FDE work, where the same idea often has to be legible to engineers, product owners, and customer stakeholders.

## Why This Strengthens My Weeks 10-11 Portfolio

Weeks 10 and 11 showed agent and evaluation work. This week made that work more credible. The Week 10 Conversion Engine is stronger when failures can be attributed to intent classification, orchestration, HubSpot/Cal.com/Resend tool behavior, runtime errors, or external state. The Week 11 judge and benchmark work is stronger when selection strategy, position bias, style-vs-reasoning slices, and source grounding are explicit.

The portfolio now signals that I can build, evaluate, explain, and debug AI systems under real constraints. That is the FDE skill set I want hiring managers to see: not only shipping a workflow, but making it observable, reproducible, and technically defensible.

## Closing Reflection

The biggest shift this week was moving from "does the system work?" to "can I explain, reproduce, and debug why it worked or failed?" Real-world AI systems need prompts and models, but they also need attribution, observability, benchmark discipline, and clear communication. This week made those capabilities visible in my portfolio.
