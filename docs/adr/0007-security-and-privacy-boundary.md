# ADR-0007: Security And Privacy Boundary

## Status

Accepted

## Context

AURA will handle personal context, memory, voice input, assistant history, and potentially sensitive user knowledge. Trust is central to commercial adoption.

## Decision

AURA's MVP security boundary is the user device.

Private user data must remain local by default. Any future external transmission of user content, memory, voice, embeddings, or assistant history requires explicit product approval, security review, and user-facing consent.

## Consequences

- Security Architecture must define data classes, local storage rules, encryption expectations, and deletion behavior.
- Logs must not contain sensitive content by default.
- Telemetry, if introduced, must be minimal, opt-in where required, and free of raw personal content.
- Claude Code tasks that touch user data must include security notes and validation steps.

## Related Documents

- `docs/05_Security/security-architecture.md`
- `docs/03_AI/memory-engine.md`
- `docs/00_Project/claude-code-task-template.md`
