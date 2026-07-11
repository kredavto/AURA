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
| v0.2 | Engineering Documentation Foundation | Make the repository navigable and decision-ready | Master Index, ADR set, documentation standards, release notes |
| v0.3 | Mobile Architecture | Define the mobile client architecture before implementation | Mobile client architecture, Android architecture, iOS architecture |
| v0.4 | AI Core And Memory | Define the AI runtime, memory, STT, TTS, and model routing | AI Core docs, Memory docs, STT/TTS architecture, Model Router architecture |
| v0.5 | Security, CI/CD, Testing | Define the safety and engineering quality foundation | Security architecture, CI/CD plan, testing strategy |
| v0.6+ | Source Code Implementation | Begin implementation from accepted architecture | Scoped implementation tasks and Pull Requests |

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
Repository v0.2: Engineering Documentation Foundation
```

v0.2 should complete the documentation and decision foundation needed before larger architecture and code implementation.

## Versioning Rule

Release versions must be documented in:

- `CHANGELOG.md`
- `ROADMAP.md`
- `releases/`

GitHub commits and Pull Requests remain the operational history.
