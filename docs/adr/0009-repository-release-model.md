# ADR-0009: Repository Release Model

## Status

Accepted

## Context

The project must not depend on chat history as storage. AURA needs a stable engineering process that future contributors and implementation agents can follow.

## Decision

AURA will progress through repository releases.

Each release must leave the repository in a coherent state with updated documentation, roadmap, changelog, and release notes. Chat messages may record discussion, but accepted project state must be represented in repository files.

## Consequences

- Repository releases are the unit of progress.
- Documentation must be updated with each completed Sprint 0 task.
- GitHub and the local project folder must stay synchronized.
- Release notes in `releases/` must explain what changed and what remains incomplete.

## Related Documents

- `docs/00_Project/project-rule-001-repository-as-source-of-truth.md`
- `docs/00_Project/repository-release-plan.md`
- `releases/v0.2.md`
- `CHANGELOG.md`
