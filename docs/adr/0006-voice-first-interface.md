# ADR-0006: Voice-First Interface

## Status

Accepted

## Context

A daily assistant must support low-friction interaction. Voice is important for mobile usage, but text must remain available for accuracy, privacy, and accessibility.

## Decision

AURA will be designed as voice-first, not voice-only.

The MVP architecture must include STT, TTS, and text interaction paths. Voice features must work locally where feasible and degrade clearly when unsupported by device capability.

## Consequences

- STT and TTS architecture must be first-class Sprint 0 documents.
- Voice UX must include cancellation, correction, and explicit user control.
- Text input/output remains mandatory for MVP.
- Voice data handling must be covered by security and privacy documentation.

## Related Documents

- `docs/03_AI/stt-engine.md`
- `docs/03_AI/tts-engine.md`
- `docs/04_Mobile/mobile-client-architecture.md`
- `docs/05_Security/security-architecture.md`
