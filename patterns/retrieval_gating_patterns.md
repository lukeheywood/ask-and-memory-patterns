# Retrieval Gating Patterns (Pattern)

This document defines concrete gating patterns used to prevent Ask systems from:
- overreaching beyond evidence
- answering from weak retrieval
- leaking private data into public surfaces

---

## Gate 1 — Policy gate (before retrieval)
Reject or narrow the query if it violates:
- topic restrictions
- data-source restrictions
- audience restrictions (public vs private)

**Output:** refusal with explicit reason.

---

## Gate 2 — Scope gate (before retrieval)
If the query is underspecified and the system requires scope:
- return a refusal asking for *scope selection*, not “more detail”

Example:
- required: which repo/collection/domain is eligible
- optional: timeframe window

---

## Gate 3 — Evidence sufficiency gate (after retrieval)
Common rules:
- minimum N sources
- minimum N distinct documents
- minimum coverage of the question’s entities

If fail:
- return “No evidence found” (not a guess)

---

## Gate 4 — Citation integrity gate (after synthesis)
Validate that:
- each strong claim has at least one citation
- citations resolve to an actual source artifact
- inference is labeled

If fail:
- downgrade to “Low” confidence and reduce claims, or refuse.

---

## Gate 5 — Leakage gate (output packaging)
If query context is “public”:
- strip any private-only sources
- refuse if removing them breaks evidence sufficiency

---

## Minimal gate report (recommended output header)

Every Ask response should include a short gate report:

- Policy: pass/fail
- Scope: what was searched
- Evidence: N docs / N sources
- Confidence: High/Medium/Low
