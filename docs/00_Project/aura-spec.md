# S0-001: AURA Specification

## Status

Accepted

## Purpose

AURA Specification is the internal project standard for creating, reviewing, and maintaining every significant artifact in the AURA repository.

It is not an application description. It is the rulebook for how AURA describes itself, how decisions are recorded, and how future contributors produce work that stays consistent over time.

## Scope

AURA Spec governs:

- architecture documents
- source code structure
- tests
- ADRs
- product requirements
- business documents
- legal drafts
- technical specifications
- implementation tasks
- tasks prepared for Claude Code
- release and version documentation

## Core Principle

No artifact should exist as an isolated opinion. Every important document, decision, task, and implementation must follow the same rules for naming, status, ownership, traceability, review, and validation.

The goal is to prevent contradictions between documents before they appear in code, product decisions, or business commitments.

## Source Of Truth

The source of truth is:

```text
GitHub repository: kredavto/AURA
Local copy: /Users/urijlebedinskij/Documents/CODEX/AURA
```

All project documents created by ChatGPT / Codex must be reflected in both locations.

## Project Rule 001

AURA does not use chat as project storage.

Chat is used for decisions, tradeoff discussion, and result verification. Accepted project state must live in the repository.

Repository releases, not isolated chat messages, are the unit of project progress.

## Required Artifact Metadata

Every major artifact must include:

- stable id
- title
- status
- purpose
- scope
- owner or responsible role
- related artifacts
- review cadence or review trigger

## Artifact Statuses

Use one of these statuses:

- `Draft`: useful but incomplete or not yet approved
- `Proposed`: ready for review
- `Accepted`: approved as current guidance
- `Superseded`: replaced by a newer artifact
- `Deprecated`: retained for history, no longer guidance

## ID System

Use stable IDs for important artifacts:

- `S0-001`: Sprint 0 standard or specification
- `PRD-001`: product requirement document
- `REQ-001`: requirement
- `ADR-0001`: architecture decision record
- `TASK-001`: implementation task
- `AI-001`: AI or agent design document
- `SEC-001`: security document
- `BUS-001`: business document
- `LEGAL-001`: legal document
- `REL-001`: release document

IDs must not be reused for a different meaning.

## File Naming

Files must use lowercase, descriptive, hyphenated names:

- `aura-spec.md`
- `development-workflow.md`
- `agent-trust-model.md`
- `privacy-model.md`
- `claude-code-task-template.md`

Avoid vague names such as:

- `notes.md`
- `final.md`
- `new-doc.md`
- `draft2.md`

## Documentation Placement

Use these locations:

- `docs/00_Project`: project rules, standards, workflows, index files
- `docs/01_Product`: PRD, MVP scope, personas, user stories, roadmap detail
- `docs/02_Architecture`: system architecture and module boundaries
- `docs/03_AI`: AI agents, model routing, prompts, evaluations, autonomy
- `docs/04_Mobile`: mobile product and platform architecture
- `docs/05_Security`: security, privacy, data classification, threat model
- `docs/06_Business`: business model, market, pricing, GTM
- `docs/07_Legal`: legal drafts and compliance planning
- `docs/adr`: final architecture decision records
- `releases`: release notes and launch checklists

## Traceability Rules

Every major implementation task must trace back to at least one product, architecture, security, AI, or business artifact.

Every major product claim must trace forward to one or more requirements or tasks before implementation starts.

Every agent autonomy change must reference:

- an AI document
- a security or privacy document
- validation criteria
- approval behavior

## Architecture Document Rules

Architecture documents must include:

- context
- problem
- decision or proposed structure
- alternatives considered when relevant
- consequences
- risks
- validation approach
- related ADRs or requirements

Architecture documents must not silently define product scope. If product scope changes, update the relevant product document.

## Code Rules

Code must be organized according to the repository structure and the current accepted architecture.

Code changes must include or reference:

- task id
- related requirement or architecture document
- validation method
- security or privacy notes when data handling changes

Implementation work should go through Pull Requests before reaching `main`.

## Test Rules

Tests must be connected to requirements or critical risks.

Test documentation must state:

- what is tested
- why it matters
- how to run it
- expected result

For AI behavior, tests should include evaluation criteria, example inputs, expected outputs, and failure modes.

## ADR Rules

ADR files must live in `docs/adr`.

Each ADR must include:

- id
- title
- status
- context
- decision
- consequences
- related documents

ADRs are for decisions that are expensive to reverse, affect multiple modules, or define long-term product/technical direction.

## Requirement Rules

Requirements must include:

- id
- user or system need
- acceptance criteria
- priority
- related artifacts
- validation method

Requirements should avoid implementation detail unless the implementation choice is itself part of the requirement.

## Business Document Rules

Business documents must include:

- purpose
- audience
- assumptions
- decision impact
- review date

Business assumptions must be marked clearly as assumptions until validated.

## Legal Document Rules

Legal documents are drafts until reviewed by qualified counsel.

Legal drafts must include:

- purpose
- jurisdiction assumptions
- data classes affected
- risk notes
- review owner

## Claude Code Task Rules

Tasks prepared for Claude Code must include:

- task id
- title
- objective
- context
- scope
- expected files
- files that must not change
- constraints
- acceptance criteria
- validation steps
- Pull Request instructions

Claude Code tasks must not silently expand scope. If implementation reveals a larger design issue, the relevant artifact must be created or updated before continuing.

## Versioning Rules

Version support is maintained through:

- `CHANGELOG.md`
- `ROADMAP.md`
- `releases/`
- GitHub commits and Pull Requests

Every release note must explain:

- what changed
- why it changed
- user or developer impact
- validation performed
- known limitations

Work must be grouped into coherent repository releases. Each release must contain a finished package of documents or implementation work that can be understood without private chat context.

## Review Rules

Review must check:

- consistency with AURA Spec
- consistency with existing architecture
- product traceability
- security and privacy impact
- Claude Code readiness when the artifact is a task

## Review Cadence

AURA Spec must be reviewed:

- before each major milestone
- before production launch
- after a major architecture change
- after security or legal review changes project rules
- when contradictions between documents are discovered

## Authority

AURA Spec is the highest-level documentation standard for the project until superseded by a later accepted specification.
