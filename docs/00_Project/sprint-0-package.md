# Sprint 0 Package

## Status

Accepted

## Method

Scrum with one-week sprints.

## Purpose

Sprint 0 is the foundation sprint for AURA. Its result is not one document, but a complete repository package that makes the project understandable, maintainable, and ready for implementation work by Claude Code and future contributors.

## Sprint Goal

Create the professional operating base for AURA:

- project standards
- master documentation index
- architecture decision records
- mobile architecture
- AI architecture
- memory engine architecture
- STT and TTS architecture
- security architecture
- task format for implementation agents
- repository versioning discipline

## Product Context

AURA is a commercial local LLM assistant for mobile devices.

It must work autonomously on user devices, including offline use without internet access. The product goal is to become a daily assistant and personal knowledge base that users trust, use frequently, and are willing to pay for.

## Backlog

| ID | Task | Status | Expected Output |
| --- | --- | --- | --- |
| S0-001 | AURA Specification | Done | `docs/00_Project/aura-spec.md` |
| S0-002 | Master Index | Planned | Repository-wide navigation and document map |
| S0-003 | ADR-0001...0010 | Planned | Ten foundational architecture decision records |
| S0-004 | Mobile Client Architecture | Planned | Cross-platform mobile architecture |
| S0-005 | Android Architecture | Planned | Android-specific architecture |
| S0-006 | iOS Architecture | Planned | iOS-specific architecture |
| S0-007 | STT Engine | Planned | Speech-to-text engine architecture |
| S0-008 | TTS Engine | Planned | Text-to-speech engine architecture |
| S0-009 | AI Model Router | Planned | AI model routing architecture |
| S0-010 | Security Architecture | Planned | Security architecture |
| S0-011 | AI Architecture | Planned | Full AI architecture |
| S0-012 | Memory Engine | Planned | Memory Engine architecture |
| S0-013 | Shared Core Architecture | Planned | Shared mobile/core architecture |

## Package Definition

Sprint 0 is complete only when the repository contains:

- a project standard
- a master index
- foundational ADRs
- mobile architecture documents
- AI engine architecture documents
- Memory Engine architecture
- STT and TTS architecture
- security architecture
- updated README
- updated CHANGELOG
- updated ROADMAP
- clear tasks for Claude Code when implementation is needed

## Working Rule

Each Sprint 0 response should complete one concrete backlog task unless the user explicitly changes the process.

Each completed task must be reflected in:

- GitHub repository `kredavto/AURA`
- local folder `/Users/urijlebedinskij/Documents/CODEX/AURA`
- `CHANGELOG.md`
- `ROADMAP.md` when status changes

## Versioning Rule

After Sprint 0 is complete, AURA should receive the next repository version, such as `v0.2.0`, with release notes in `releases/`.

Sprint 0 work should feed into `Repository v0.2: Engineering Documentation Foundation`.

Project progress is measured by completed repository releases, not by chat messages or isolated documents.

## Definition Of Done

A Sprint 0 task is done when:

- the expected document exists in the correct repository section
- the document follows AURA Spec
- related indexes or roadmap entries are updated
- the same content exists locally and in GitHub
- the result is clear enough for Claude Code or another contributor to continue without private chat context
- Claude Code can start implementation without making major architecture decisions
