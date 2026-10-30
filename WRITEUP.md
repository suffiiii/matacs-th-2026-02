# AI Proposal Triage System - Design Write-Up

### 1. AI vs. Rules
AI is used **only for unstructured data extraction** from uploaded proposal PDFs (converting plain text into a structured JSON schema). Deterministic code/rules handle **validation, mandatory pass/fail checks, mathematical score calculation, and final ranking**. We draw the line here because LLMs struggle with precise arithmetic consistency and strict boolean compliance, whereas rule-based engines guarantee 100% mathematical repeatability.

### 2. Consistency & Explainability
Scores are fully repeatable because scoring formulas (e.g., linear interpolation for price/timeline and weighted sums) are executed by code, not LLM generations. Temperature is set to `0.0` during extraction. Every ranked item includes a detailed audit breakdown showing raw extracted values, mandatory pass/fail status, individual weighted sub-scores, and clear explanatory notes for reviewers.

### 3. Human in the Loop
A reviewer sees an interactive dashboard displaying auto-calculated ranks, flagged items, and extracted evidence side-by-side with original PDFs. Humans retain full control to:
- Confirm or override pass/fail statuses.
- Review security flags (e.g., prompt injections).
- Make final award decisions.
All human actions, manual score overrides, and timestamped justifications are stored in an immutable audit log database.

### 4. Changing Criteria
If an admin modifies criteria or weightings after scoring, the system retains previously extracted JSON data. It does NOT re-run AI extraction (saving cost/time); instead, the rule engine re-runs scoring logic against existing JSON records and notifies the reviewer of updated rankings.

### 5. Risks & Guardrails
- **Prompt Injection / Manipulation:** Guardrailed using strict JSON schemas, system-level safety prompts, pre-scoring security pipelines, and heuristic filters flagging adversarial phrases (e.g., Proposal C).
- **Hallucinations / False Extraction:** AI outputs structured JSON; validation code checks types/ranges and links extracted facts to source document text spans for human verification.
- **Cost & Latency:** Cheap, fast extraction models (e.g., Claude Haiku / GPT-4o-mini) are used with cached system prompts.