# Project Rule 001: Repository As Source Of Truth

## Status

Accepted

## Purpose

AURA must not use chat history as project storage.

Chat is for decisions, review, and result verification. The project itself must exist as a real repository with durable files, version history, release notes, and reviewable changes.

## Rule

The AURA project lives in:

```text
GitHub repository: kredavto/AURA
Local copy: /Users/urijlebedinskij/Documents/CODEX/AURA
```

The chat is not a source of truth.

## What Chat Is Used For

Chat may be used for:

- making decisions
- discussing tradeoffs
- reviewing proposed outputs
- checking whether a repository release is complete
- giving instructions to ChatGPT / Codex or Claude Code

## What Chat Is Not Used For

Chat must not be used as:

- long-term documentation storage
- the only copy of product decisions
- the only place where architecture exists
- the only place where tasks for Claude Code exist
- the only place where release scope is defined

## Repository Release Model

AURA will move by repository releases, not by isolated chat messages or one-off documents.

Each release must contain a coherent package of documents or implementation work that is ready to use without private chat context.

Example release sequence:

- `Repository v0.2`: engineering documentation foundation
- `Repository v0.3`: mobile architecture
- `Repository v0.4`: AI Core and Memory
- `Repository v0.5`: security, CI/CD, and testing
- later releases: source code implementation

## Release Requirements

Each repository release must include:

- clear release goal
- included documents or code areas
- updated README when navigation changes
- updated CHANGELOG
- updated ROADMAP
- release notes in `releases/`
- validation notes
- known limitations

## Working Rule

Before starting a new package of work, define which repository release it belongs to.

If a decision is made in chat, it must be reflected in the repository before it is treated as accepted project state.

## Technical Product Manager Check

Every release must be checked against:

- commercial launch progress
- MVP scope discipline
- architecture simplicity
- documentation consistency
- readiness for Claude Code or future contributors
- path toward first paying customers
