# Sources — Failure Attribution in Multi-Agent LLM Systems

## Primary Papers

1. Who&When: Automated Failure Attribution in LLM Multi-Agent Systems
   - ICML 2025
   - Core contribution:
     Formalizes automated failure attribution for multi-agent systems by identifying:
       - responsible agent
       - failure step
       - failure reasoning
   - Introduces:
       - All-at-once attribution
       - Step-by-step attribution
       - Binary-search attribution

2. Zheng et al. — Judging LLM-as-a-Judge with MT-Bench and Chatbot Arena
   - Introduces limitations of LLM judges:
       - position bias
       - verbosity bias
       - self-enhancement bias

3. Gu et al. — A Survey on LLM-as-a-Judge
   - Explains evaluation reliability problems in automated judging systems.

---

# Concepts Connected to the Explainer

## Failure Attribution
Failure attribution identifies:
- which component failed,
- at which step,
- and why.

This differs from simple outcome evaluation.

---

## Agent Observability
Modern agent systems require:
- structured traces,
- typed tool outputs,
- causal execution records,
- replayable workflows.

---

## pass@k Evaluation
pass@k measures:
- whether a system can solve a task across multiple attempts.

This requires:
- independent trials,
- grouped runs,
- stable trace logging.

---

## Bootstrap Confidence Intervals
Bootstrap CI estimates uncertainty in benchmark results.

Requires:
- task-level outcome records,
- reproducible evaluation samples.

---

# Tooling / Repo Grounding

Relevant repo areas:
- conversion_engine_backend/main.py
- llm/prompts.py
- services/hubspot_service.py
- services/cal_service.py
- services/email_service.py
- eval/harness.py

Key missing layer:
- structured causal trace schema