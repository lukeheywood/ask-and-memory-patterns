# Ask & Memory Patterns

**Purpose:** Concrete design patterns for “Ask systems” — how a question becomes a bounded retrieval + answer process that remains **traceable, reviewable, and resistant to overreach**.

**Audience:** Senior engineers, architects, technical hiring managers.

**This is a glass case repo.** It contains *patterns and artifacts*, not runtime systems.

---

## What this repo is

An **Ask system** is a deterministic wrapper around retrieval + answering. It is not “RAG” as a feature — it is an interface contract that:

- defines what the user is allowed to ask
- defines what “memory” is for the system
- enforces retrieval boundaries and evidence requirements
- returns an answer **with provenance** (where it came from) or a refusal

This repo documents patterns that can be implemented in any stack.

---

## What this repo is not

- Not a model benchmark or prompt collection
- Not an agent framework
- Not an implementation of ONE’s private memory vault
- Not a claim that answers are always correct — only that they are **bounded and evidencable**

---

## Contents

### Patterns (core exhibits)
- `patterns/ask_system_pipeline.md` — a concrete Ask pipeline (inputs/outputs, steps, failure modes)
- `patterns/memory_evidence_contract.md` — what “valid memory” means (artifact contract + provenance)
- `patterns/retrieval_gating_patterns.md` — boundary enforcement patterns (pre/post gates)

---

## Relationship to ONE

- Canonical hub (System Atlas): **`one-platform`**
- This repo is an “exhibit shelf”: reusable Ask/memory patterns that support the Atlas.

If you are trying to understand ONE end-to-end, start at `one-platform`.

---

## Status

**Stage:** Stage-1 (glass case aligned)  
**Last verified:** 2026-01-01

Patterns are intentionally minimal and concrete. Depth increases only when a pattern is stable enough to publish without drift.

