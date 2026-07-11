# AURA

AURA is a local-first AI assistant platform.

This repository is organized as a production-grade foundation for product, architecture, AI, mobile, backend, security, business, legal, release, and engineering work.

## Repository Structure

```text
AURA/
├── .github/
│   ├── ISSUE_TEMPLATE/
│   ├── PULL_REQUEST_TEMPLATE.md
│   └── workflows/
├── docs/
│   ├── 00_Project/
│   ├── 01_Product/
│   ├── 02_Architecture/
│   ├── 03_AI/
│   ├── 04_Mobile/
│   ├── 05_Security/
│   ├── 06_Business/
│   ├── 07_Legal/
│   └── adr/
├── src/
├── mobile/
├── backend/
├── ai/
├── tests/
├── scripts/
├── assets/
├── releases/
├── README.md
├── CHANGELOG.md
├── CONTRIBUTING.md
├── LICENSE
└── ROADMAP.md
```

## Operating Roles

ChatGPT / Codex owns repository structure, documentation, version support, README, CHANGELOG, and task preparation for Claude Code.

ChatGPT / Codex also acts as Technical Product Manager: keeping architecture simple, documentation consistent, MVP scope controlled, and development focused on commercial launch.

Claude Code owns implementation work through scoped branches and Pull Requests.

See:

- [docs/00_Project/aura-spec.md](docs/00_Project/aura-spec.md)
- [docs/00_Project/project-rule-001-repository-as-source-of-truth.md](docs/00_Project/project-rule-001-repository-as-source-of-truth.md)
- [docs/00_Project/repository-release-plan.md](docs/00_Project/repository-release-plan.md)
- [docs/00_Project/sprint-0-package.md](docs/00_Project/sprint-0-package.md)
- [docs/00_Project/sprint-0-foundation-repository.md](docs/00_Project/sprint-0-foundation-repository.md)
- [docs/00_Project/operating-responsibilities.md](docs/00_Project/operating-responsibilities.md)
- [docs/00_Project/technical-product-management.md](docs/00_Project/technical-product-management.md)
- [docs/00_Project/claude-code-task-template.md](docs/00_Project/claude-code-task-template.md)

## Repository Releases

AURA progresses through complete repository releases, not isolated chat messages.

Current target:

```text
Repository v0.2: Foundation Repository
```

## Product Direction

AURA is a commercial local LLM assistant for mobile devices. It must work autonomously on user devices, including offline use without internet access, and become a daily assistant and personal knowledge base that users trust and are willing to pay for.

Before active code development, AURA must complete a value proposition validation stage with potential users.
