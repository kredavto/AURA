# Repository Release Plan

## Status

Accepted

## Purpose

This document defines how AURA moves forward through complete repository releases instead of isolated documents.

## Release Philosophy

AURA will be developed as a real product repository. Each release must leave the repository in a more complete, coherent, and usable state.

The release unit is a finished package of repository content, not a chat answer.

## Planned Releases

| Release | Theme | Purpose | Output |
| --- | --- | --- | --- |
| v0.2 | Foundation Repository | Complete Sprint 0 foundation before coding | Master Index, ADRs, mobile architecture, AI architecture, Memory, STT, TTS, model router, security architecture |
| v0.3 | Value Proposition Validation | Test market demand before active code development | User interviews, segment hypotheses, value proposition evidence, MVP scope recommendations |
| v0.4 | Implementation Preparation | Prepare Claude Code implementation tasks | Feature backlog, task specs, implementation sequencing |
| v0.5 | MVP Source Code Foundation | Begin implementation from accepted architecture and validated value proposition | Mobile shared core, local runtime skeleton, tests |
| v0.6 | Private Alpha Readiness | Make the first user-testable local assistant build | Offline assistant loop, memory prototype, security baseline |
| v0.7+ | Commercial MVP | Move toward first paying customers | Launch-critical features, packaging, onboarding, payments when ready |

## Release Completion Criteria

Each release is complete when:

- all planned artifacts exist in the repository
- all artifacts follow AURA Spec
- README navigation is updated if needed
- CHANGELOG is updated
- ROADMAP is updated
- release notes exist in `releases/`
- Claude Code can continue from repository context alone

## Current Release Target

The current target is:

```text
Repository v0.2: Foundation Repository
```

v0.2 should complete Sprint 0: the repository, documentation, decisions, mobile architecture, AI architecture, memory, speech, and security foundation needed before source code implementation.

Active code development should not begin until `Repository v0.3: Value Proposition Validation` provides enough evidence that the product direction is wanted by a real target segment.

## Versioning Rule

Release versions must be documented in:

- `CHANGELOG.md`
- `ROADMAP.md`
- `releases/`

GitHub commits and Pull Requests remain the operational history.
