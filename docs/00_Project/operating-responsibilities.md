# Operating Responsibilities

## Status

Accepted

## Purpose

This document fixes the working responsibility model for AURA so the repository can be maintained consistently while implementation work is delegated through Pull Requests.

## Source Of Truth

GitHub repository `kredavto/AURA` is the source of truth for project structure, documentation, tasks, code, reviews, releases, and change history.

Local project files are also maintained in:

```text
/Users/urijlebedinskij/Documents/CODEX/AURA
```

## ChatGPT / Codex Responsibilities

ChatGPT / Codex owns:

- creating and maintaining repository structure
- placing and organizing all project documentation
- supporting versions and release notes
- maintaining `README.md`
- maintaining `CHANGELOG.md`
- preparing implementation tasks for Claude Code
- preparing architecture documents, PRD, ADR, specifications, and review notes
- keeping documentation traceable and consistent with AURA Spec

## Claude Code Responsibilities

Claude Code owns:

- implementation work
- code changes
- tests
- build scripts
- CI/CD implementation
- bug fixes assigned through prepared tasks
- Pull Requests for scoped implementation work

## Pull Request Rule

All implementation work should go through Pull Requests before reaching `main`.

Each task prepared for Claude Code must include:

- task id
- objective
- scope
- expected files
- constraints
- acceptance criteria
- validation steps
- target branch or Pull Request instructions

## Maintenance Rule

When ChatGPT / Codex creates or updates project files, the change should be reflected in both:

- GitHub repository `kredavto/AURA`
- local folder `/Users/urijlebedinskij/Documents/CODEX/AURA`
