# ADR-0010: Claude Code Implementation Boundary

## Status

Accepted

## Context

AURA uses a workflow where ChatGPT / Codex owns architecture, documentation, product guardrails, and implementation task preparation, while Claude Code performs scoped implementation work.

Without a clear boundary, implementation agents may make product or architecture decisions implicitly in code.

## Decision

Claude Code implementation work must be driven by repository artifacts and scoped tasks.

Claude Code may write code, tests, CI, scripts, and implementation documentation within an approved task. It must not introduce major architecture, product scope, privacy, security, or business model decisions without a corresponding repository artifact update and review.

## Consequences

- Claude Code tasks must use the project task template.
- Pull Requests must reference relevant ADRs and documents.
- If implementation exposes a missing decision, the decision must be documented before broad implementation continues.
- ChatGPT / Codex remains responsible for keeping architecture and product scope coherent.

## Related Documents

- `docs/00_Project/claude-code-task-template.md`
- `docs/00_Project/operating-responsibilities.md`
- `docs/00_Project/technical-product-management.md`
- `.github/PULL_REQUEST_TEMPLATE.md`
