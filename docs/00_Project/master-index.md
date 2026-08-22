# S0-002: Master Index

## Status

Accepted

## Purpose

Master Index is the top-level navigation map for AURA.

It exists so ChatGPT / Codex, Claude Code, future contributors, and reviewers can understand the repository without relying on chat history.

## Source Of Truth

```text
GitHub repository: kredavto/AURA
Local copy: /Users/urijlebedinskij/Documents/CODEX/AURA
```

The chat is not a source of truth. Accepted project state must be reflected in repository files.

## Current Product Direction

AURA is a commercial local LLM assistant for mobile devices.

Core product constraints:

- offline-first operation
- autonomous local operation on user devices
- daily assistant use case
- personal knowledge base behavior
- privacy-preserving local memory
- voice and text interaction
- value proposition validation before active code development

## Current Release Target

```text
Repository v0.2: Foundation Repository
```

The goal of v0.2 is to complete the foundation needed before Claude Code starts implementation planning.

## Repository Root

| Path | Purpose | Status |
| --- | --- | --- |
| `README.md` | Repository overview and primary entry point | Active |
| `CHANGELOG.md` | Change history | Active |
| `ROADMAP.md` | Release and project roadmap | Active |
| `CONTRIBUTING.md` | Contribution rules | Active |
| `LICENSE` | Proprietary license notice | Active |

## Project Rules And Operations

| Path | Purpose | Status |
| --- | --- | --- |
| `docs/00_Project/aura-spec.md` | S0-001 internal project standard | Accepted |
| `docs/00_Project/master-index.md` | S0-002 repository navigation map | Accepted |
| `docs/00_Project/project-rule-001-repository-as-source-of-truth.md` | Rule that repository is source of truth, not chat | Accepted |
| `docs/00_Project/repository-release-plan.md` | Release-based project workflow | Accepted |
| `docs/00_Project/sprint-0-foundation-repository.md` | Scrum plan for Sprint 0 | Accepted |
| `docs/00_Project/sprint-0-package.md` | Sprint 0 package definition and backlog | Accepted |
| `docs/00_Project/operating-responsibilities.md` | ChatGPT / Codex, Claude Code, and repository responsibilities | Accepted |
| `docs/00_Project/technical-product-management.md` | TPM guardrails and commercial focus | Accepted |
| `docs/00_Project/claude-code-task-template.md` | Standard task format for Claude Code | Accepted |

## Product

| Path | Purpose | Status |
| --- | --- | --- |
| `docs/01_Product/README.md` | Product section index | Active |
| `docs/01_Product/value-proposition-validation.md` | Required discovery gate before active code development | Accepted |
| `docs/product-brief.md` | Early product brief | Draft |

## Architecture

| Path | Purpose | Status |
| --- | --- | --- |
| `docs/02_Architecture/README.md` | Architecture section index | Active |
| `docs/02_Architecture/shared-core-architecture.md` | Shared architecture core for mobile, AI, memory, speech, and security boundaries | Accepted |
| `docs/adr/README.md` | Architecture Decision Records section index | Active |
| `docs/adr/0001-local-first-mobile-llm.md` | Local-first mobile LLM decision | Accepted |
| `docs/adr/0002-offline-first-operation.md` | Offline-first operation decision | Accepted |
| `docs/adr/0003-local-memory-first.md` | Local memory first decision | Accepted |
| `docs/adr/0004-mobile-platform-split.md` | Shared architecture with platform-specific Android/iOS plans | Accepted |
| `docs/adr/0005-on-device-model-runtime.md` | On-device runtime as core system component | Accepted |
| `docs/adr/0006-voice-first-interface.md` | Voice-first, not voice-only, interaction model | Accepted |
| `docs/adr/0007-security-and-privacy-boundary.md` | Device as MVP security boundary | Accepted |
| `docs/adr/0008-value-proposition-before-code.md` | Validation stage before active code development | Accepted |
| `docs/adr/0009-repository-release-model.md` | Repository releases as unit of progress | Accepted |
| `docs/adr/0010-claude-code-implementation-boundary.md` | Implementation agent decision boundary | Accepted |

## AI

| Path | Purpose | Status |
| --- | --- | --- |
| `docs/03_AI/README.md` | AI section index | Active |
| `ai/README.md` | Future AI-core code area | Placeholder |

Planned Sprint 0 outputs:

- `docs/03_AI/ai-architecture.md`
- `docs/03_AI/memory-engine.md`
- `docs/03_AI/stt-engine.md`
- `docs/03_AI/tts-engine.md`
- `docs/03_AI/ai-model-router.md`

## Mobile

| Path | Purpose | Status |
| --- | --- | --- |
| `docs/04_Mobile/README.md` | Mobile documentation index | Active |
| `docs/04_Mobile/mobile-client-architecture.md` | Cross-platform mobile client architecture | Accepted |
| `docs/04_Mobile/android-architecture.md` | Android-specific architecture | Accepted |
| `mobile/README.md` | Future mobile code area | Placeholder |

Planned Sprint 0 output:

- `docs/04_Mobile/ios-architecture.md`

## Security

| Path | Purpose | Status |
| --- | --- | --- |
| `docs/05_Security/README.md` | Security documentation index | Active |

Planned Sprint 0 output:

- `docs/05_Security/security-architecture.md`

## Business And Legal

| Path | Purpose | Status |
| --- | --- | --- |
| `docs/06_Business/README.md` | Business documentation index | Active |
| `docs/07_Legal/README.md` | Legal documentation index | Active |

## Engineering Areas

| Path | Purpose | Status |
| --- | --- | --- |
| `src/README.md` | Future application source area | Placeholder |
| `backend/README.md` | Future backend services area | Placeholder |
| `tests/README.md` | Future tests area | Placeholder |
| `scripts/README.md` | Future automation scripts area | Placeholder |
| `assets/README.md` | Product and brand assets | Placeholder |

## Releases

| Path | Purpose | Status |
| --- | --- | --- |
| `releases/README.md` | Release section index | Active |
| `releases/v0.2.md` | Planned Foundation Repository release notes | Planned |

## Sprint 0 Status

| ID | Task | Status |
| --- | --- | --- |
| S0-001 | AURA Spec | Done |
| S0-002 | Master Index | Done |
| S0-003 | ADR-0001...0010 | Done |
| S0-004 | Mobile Client Architecture | Done |
| S0-005 | Android Architecture | Done |
| S0-006 | iOS Architecture | Planned |
| S0-007 | STT Engine | Planned |
| S0-008 | TTS Engine | Planned |
| S0-009 | AI Model Router | Planned |
| S0-010 | Security Architecture | Planned |
| S0-011 | AI Architecture | Planned |
| S0-012 | Memory Engine | Planned |
| S0-013 | Shared Core Architecture | Done |

## Next Recommended Task

Next task:

```text
S0-006: iOS Architecture
```

Reason: iOS architecture should now mirror the Android level of specificity while respecting iOS runtime, storage, permission, and speech constraints.
