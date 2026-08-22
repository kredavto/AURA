# ADR-0003: Local Memory First

## Status

Accepted

## Context

AURA must become a personal knowledge base and daily assistant. This requires memory, but memory is also the highest-risk area for privacy, trust, and user control.

## Decision

AURA memory will be local-first.

User memories, embeddings, summaries, preferences, and retrieved personal context must be stored on device by default. The MVP must provide explicit user control over what is remembered, edited, deleted, and used in responses.

Cloud memory is not part of the MVP baseline.

## Consequences

- Memory design must include lifecycle, deletion, export, and reset behavior.
- Retrieval quality must be balanced against storage size and on-device performance.
- Sensitive memory classes must be defined before implementation.
- The assistant must be able to answer without memory when the user disables it.

## Related Documents

- `docs/03_AI/memory-engine.md`
- `docs/05_Security/security-architecture.md`
- `docs/01_Product/value-proposition-validation.md`
