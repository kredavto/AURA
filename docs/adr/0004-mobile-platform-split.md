# ADR-0004: Mobile Platform Split

## Status

Accepted

## Context

AURA targets mobile users. Android and iOS have different model runtime options, security APIs, background execution limits, speech APIs, file systems, and performance constraints.

Forcing all mobile behavior into one cross-platform abstraction too early would hide critical platform decisions.

## Decision

AURA will use a shared product and architecture model, with platform-specific Android and iOS implementation plans.

The repository will document:

- shared mobile architecture
- Android-specific architecture
- iOS-specific architecture

Cross-platform reuse is allowed when it does not weaken platform performance, security, or user experience.

## Consequences

- Mobile architecture must separate shared concepts from platform execution details.
- Claude Code tasks must specify target platform and files.
- Platform-specific model runtime decisions may differ between Android and iOS.
- MVP sequencing may start with one platform if value validation supports that choice.

## Related Documents

- `docs/04_Mobile/mobile-client-architecture.md`
- `docs/04_Mobile/android-architecture.md`
- `docs/04_Mobile/ios-architecture.md`
- `docs/02_Architecture/shared-core-architecture.md`
