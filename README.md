# ONE — Ask and Memory Patterns

This repository contains design patterns for **Ask systems** that use memory responsibly.

It focuses on how systems retrieve context, ground answers, and remain explainable — not on producing fluent responses at any cost.

Memory here is structural.
Asking is constrained.

---

## 🧭 What this repo is

Ask and memory patterns define how a system:

- Decides what context may be retrieved
- Separates stored knowledge from generated output
- Preserves traceability between inputs, memory, and answers
- Prevents plausible but ungrounded responses

These patterns exist to ensure that answers remain **accountable**, not just helpful.

---

## 🧱 What lives in this repository

This repository includes patterns for:

- Memory indexing and segmentation
- Retrieval boundaries and eligibility rules
- Ask flows that distinguish:
  - retrieval,
  - synthesis,
  - and presentation
- Guardrails that prevent memory misuse or overreach

These patterns are intentionally:

- Model-agnostic
- Storage-agnostic
- Resistant to “just ask the LLM” shortcuts

They define *how asking is allowed to work*.

---

## 🔍 Relationship to ONE

Within the broader ONE system:

- `system-skeletons` defines allowed shapes for memory and Ask
- `contract-stack-examples` constrains how retrieval and synthesis may occur
- `ask-and-memory-patterns` defines **how questions are answered**
- `ai-workflow-engine` executes Ask flows as pipelines
- `one-reference-system` inspects what was retrieved and why

This repository ensures that asking never bypasses structure.

---

## 📌 Concrete example

A pattern in this repository may specify that:

- A question must declare its intent
- Only memory entries tagged as eligible may be retrieved
- Retrieved context is passed separately from the question
- The system must distinguish cited context from generated synthesis

The result is not the *best sounding* answer,  
but the **most accountable one**.

---

## 🚧 Status & intent

Ask systems evolve as memory grows.

This repository prioritises restraint, clarity, and traceability.
Patterns here are designed to prevent systems from confidently answering questions they do not have the right to answer.

The goal is not confidence.
The goal is **answerability with integrity**.

---

*If memory is what a system knows,  
asking is how it chooses to speak.*
---

## 📚 ONE — Repository Index

- **system-skeletons** → Structural blueprints and allowed system shapes  
- **contract-stack-examples** → Formal invariants and governance constraints  
- **one-reference-system** → System inspection and explainability anchor  
- **ai-workflow-engine** → Governed, artifact-producing execution pipelines  
- **system-diagnostics** → Mapping and drift-detection patterns  
- **ask-and-memory-patterns** → Grounded retrieval and answerability design

This index exists for orientation only.  
Each repository remains independently scoped and truth-aligned.
