# Memory Evidence Contract (Pattern)

This document defines what counts as **valid memory** for an Ask system.
It is a contract between ingestion and retrieval.

---

## Definitions

### Memory (in this repo)
A *retrievable artifact* eligible to answer questions.
Memory is not “anything stored” — it is **eligible evidence**.

### Evidence
A memory item used to justify a claim in an answer.

---

## Minimum fields for a memory artifact

A memory item is eligible only if it has:

1. **Stable identifier**
   - unique ID (hash or deterministic ID)
2. **Source**
   - where it came from (repo path, doc URL, export file)
3. **Timestamp**
   - creation time or event time (if known)
4. **Scope tags**
   - domain/collection classification
5. **Redaction status** (if relevant)
   - public-safe vs private-only

Optional but recommended:
- owner (who can vouch for it)
- lifecycle state: `draft | active | deprecated`

---

## Provenance requirements (for citation)

A citation must allow a reviewer to:
- locate the source artifact
- locate the specific section (line range, heading, page)
- verify the claim without model interpretation

If your system cannot produce that, it must not claim provenance.

---

## Eligibility rules (example set)

A memory item is **ineligible** if:
- it is missing source info
- it is missing timestamp (when the question requires recency)
- it is marked deprecated
- it is private-only and the query context is public

---

## Why this contract exists

Without a deterministic semantic contract:
- embeddings represent similarity, not intent
- retrieval returns plausible text, not “truth”
- answers drift because the system can’t distinguish evidence from noise

The contract forces “memory” to be **owned, scoped, and reviewable**.
