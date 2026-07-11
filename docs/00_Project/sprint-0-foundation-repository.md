# Sprint 0: Foundation Repository

## Status

Accepted

## Method

Scrum with one-week sprints.

## Sprint Goal

Create the full project foundation so Claude Code can start writing code after Sprint 0 with minimal independent architecture decisions.

Sprint 0 must turn AURA into a repository-first product project with enough documentation, decisions, and boundaries to support implementation work.

## Product Context

AURA is a commercial product: a local LLM assistant that runs autonomously on users' mobile devices, including offline use without internet access.

The product should become a daily assistant and personal knowledge base that users can ask about anything, like an experienced helper that understands their context while preserving privacy and local control.

## Product Goal

Bring AURA to market as a real product that people use daily and are willing to pay for.

## Sprint Scope

Sprint 0 includes:

1. Repository foundation
2. AURA Spec
3. Master Index
4. Architecture Decision Records
5. Mobile Architecture
6. AI Architecture
7. Memory Engine
8. STT Engine
9. TTS Engine
10. Security Architecture

## Sprint Backlog

| ID | Task | Status | Output |
| --- | --- | --- | --- |
| S0-001 | AURA Spec | Done | `docs/00_Project/aura-spec.md` |
| S0-002 | Master Index | Planned | `docs/00_Project/master-index.md` |
| S0-003 | ADR-0001...0010 | Planned | `docs/adr/` |
| S0-004 | Mobile Client Architecture | Planned | `docs/04_Mobile/mobile-client-architecture.md` |
| S0-005 | Android Architecture | Planned | `docs/04_Mobile/android-architecture.md` |
| S0-006 | iOS Architecture | Planned | `docs/04_Mobile/ios-architecture.md` |
| S0-007 | STT Engine | Planned | `docs/03_AI/stt-engine.md` |
| S0-008 | TTS Engine | Planned | `docs/03_AI/tts-engine.md` |
| S0-009 | AI Model Router | Planned | `docs/03_AI/ai-model-router.md` |
| S0-010 | Security Architecture | Planned | `docs/05_Security/security-architecture.md` |
| S0-011 | AI Architecture | Planned | `docs/03_AI/ai-architecture.md` |
| S0-012 | Memory Engine | Planned | `docs/03_AI/memory-engine.md` |
| S0-013 | Shared Core Architecture | Planned | `docs/02_Architecture/shared-core-architecture.md` |

## Definition Of Done

Sprint 0 is complete when:

- repository structure is stable
- AURA Spec is accepted
- Master Index maps the full repository
- foundational ADRs are accepted
- mobile architecture is documented for shared core, Android, and iOS
- AI architecture is documented
- Memory Engine is documented
- STT Engine is documented
- TTS Engine is documented
- AI Model Router is documented
- Security Architecture is documented
- README, CHANGELOG, ROADMAP, and release notes are updated
- Claude Code can begin implementation without making major architecture decisions

## Out Of Scope

Sprint 0 does not include:

- production app implementation
- model training
- backend implementation
- mobile app code
- payment implementation
- public launch

## Product Management Guardrails

Sprint 0 decisions must support:

- offline-first mobile operation
- local privacy and user control
- daily user engagement
- commercial launch readiness
- minimum viable product scope
- architecture simplicity

Avoid:

- speculative enterprise features
- premature cloud dependence
- unnecessary platform abstractions
- AI autonomy without explicit control rules
- features that do not help reach first paying users

## Review

At the end of Sprint 0, repository v0.2 must be reviewed as a whole package, not as separate documents.
