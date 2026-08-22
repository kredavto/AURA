# ADR-0002: Offline-First Operation

## Status

Accepted

## Context

AURA must work autonomously on mobile devices even without internet access.

Offline capability is not a secondary convenience. It is part of the product's value proposition: privacy, reliability, and daily availability.

## Decision

AURA will be offline-first for the MVP.

The MVP must support a complete local assistant session without network access, including text interaction, local memory retrieval, and local response generation.

Network-dependent features are out of scope for the first implementation phase unless they are optional and do not block the assistant loop.

## Consequences

- Core product flows must be tested in airplane-mode conditions.
- Error handling must assume network absence as normal behavior.
- Sync, cloud backup, server-side personalization, and remote model calls are non-MVP unless explicitly re-approved.
- Offline evaluation scenarios must be included before private alpha readiness.

## Related Documents

- `docs/00_Project/aura-spec.md`
- `docs/00_Project/sprint-0-foundation-repository.md`
- `docs/05_Security/security-architecture.md`
- `docs/03_AI/ai-model-router.md`
