# Ask System Pipeline (Pattern)

This document defines a concrete, implementation-agnostic **Ask pipeline**.
It is written as a black-and-white sequence: inputs, steps, outputs, failure modes.

---

## Inputs (required)

1. **User question** (string)
2. **Query context** (optional)
   - scope (collection(s), domain)
   - timeframe constraint (if any)
   - audience constraint (public/private)
3. **System policy**
   - what data sources are eligible
   - what topics are prohibited
   - what must be cited

---

## Outputs (required)

An Ask system must return exactly one of:

### A) Answer with evidence
- Answer text
- Evidence bundle (citations / references)
- Confidence class (not probability): `High | Medium | Low`
- Coverage note: what was and wasn’t searched

### B) Refusal (bounded)
- Refusal reason (policy / missing data / ambiguity)
- What would be needed to answer (specific missing artifact, not “more detail”)

### C) “No evidence found”
- Explicit statement that no eligible evidence was retrieved
- Optional suggested next action (e.g., ingest missing doc)

---

## Pipeline (deterministic sequence)

### Step 0 — Normalize question
- Trim, de-noise, detect language
- Extract explicit constraints (dates, entities)

**Fail mode:** hidden assumptions (e.g., the system invents constraints)
**Mitigation:** constraints must be echoed back in the output header (coverage note).

### Step 1 — Intent translation (bounded)
Translate the question into:
- target domain(s)
- retrieval filters (if any)
- “evidence required” level

**Rule:** intent translation is not allowed to expand scope beyond policy.

### Step 2 — Eligibility gate (pre-retrieval)
Reject or narrow if:
- question violates policy
- scope is undefined and policy requires it
- requested evidence type is unavailable

### Step 3 — Retrieval
Retrieve candidate chunks/documents from eligible sources.

**Output artifact:** `retrieval_set`
- list of retrieved items
- scores / ranks (if available)
- source identifiers

### Step 4 — Evidence gate (post-retrieval)
Validate the retrieval set:
- minimum number of sources (if required)
- diversity (avoid single-source hallucination)
- recency rules (if configured)
- provenance completeness

If it fails: return “No evidence found” or “Refusal: missing evidence”.

### Step 5 — Answer synthesis (bounded)
Generate answer strictly from retrieval_set.

**Rules:**
- No new facts without evidence
- Any inference must be labeled as inference
- If evidence conflicts, present both

### Step 6 — Output packaging
Return:
- answer
- citations
- coverage note
- confidence class

---

## Minimal acceptance checklist

An Ask answer is acceptable only if:
- [ ] It includes citations or explicitly says none were found
- [ ] It states what corpus/scope was searched
- [ ] It does not introduce uncited facts
- [ ] It labels inference vs citation-backed claims
- [ ] It does not exceed policy scope

---

## Notes

This pattern is intentionally compatible with:
- RAG over vector stores
- keyword search
- hybrid retrieval
- human-curated memory stores
