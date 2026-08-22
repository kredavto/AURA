# ADR-0001: Local-First Mobile LLM

## Status

Accepted

## Context

AURA is intended to become a commercial daily assistant and personal knowledge base that runs on user-owned mobile devices.

The product must be useful without requiring constant network access, and user trust depends on keeping sensitive context under local control.

## Decision

AURA will be designed as a local-first mobile LLM product.

The primary assistant loop, user context, memory access, and core inference path must run on the user's mobile device whenever supported by device capability.

Cloud services may be introduced later only as optional extensions, not as a requirement for the MVP assistant loop.

## Consequences

- Mobile runtime constraints become a primary architecture input.
- Model size, quantization, latency, memory pressure, and battery use must be treated as product constraints.
- The MVP must avoid features that depend on always-online cloud inference.
- Product claims must clearly distinguish local behavior from optional future network behavior.

## Related Documents

- `docs/00_Project/aura-spec.md`
- `docs/00_Project/master-index.md`
- `docs/01_Product/value-proposition-validation.md`
- `docs/04_Mobile/mobile-client-architecture.md`
- `docs/03_AI/ai-architecture.md`
