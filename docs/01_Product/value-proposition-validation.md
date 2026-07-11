# Value Proposition Validation

## Status

Accepted

## Purpose

AURA must validate its value proposition with potential users before active code development begins.

This does not pause the project. It means product design and market validation run in parallel so AURA does not become a technically strong system without a real market.

## Rule

Before active implementation starts, AURA must complete a dedicated value proposition validation stage.

This stage must test whether potential users understand, need, trust, and would pay for a local offline-first LLM assistant on mobile devices.

## Product Hypothesis

AURA is a commercial local LLM assistant that runs autonomously on mobile devices, works without internet access, and becomes a daily assistant and personal knowledge base.

Target users should see AURA as:

- useful every day
- safer than cloud-only assistants
- personal enough to become a knowledge base
- reliable when offline
- valuable enough to pay for

## Key Validation Questions

- Who has the strongest pain that AURA solves?
- What daily situations would make users open AURA?
- Is offline local operation a must-have, a differentiator, or only a nice-to-have?
- What data would users trust AURA with?
- What would users not trust AURA with?
- Which first use case creates a strong habit?
- What would make users pay?
- What price range feels reasonable?
- What would block adoption?

## Target Interview Segments

Initial validation should include:

- founders and solo operators
- consultants and knowledge workers
- creators and researchers
- people who often work with sensitive personal or business information
- users who already rely on AI assistants but worry about privacy or continuity

## Validation Methods

Use lightweight validation before code:

- problem interviews
- landing page or concept test
- clickable mockup or narrative demo
- willingness-to-pay conversations
- competitor comparison interviews
- manual concierge workflow if useful

## Evidence Required

Before active code development, the repository should contain:

- interview notes or summaries
- user segment hypotheses
- top user pains
- strongest use cases
- pricing assumptions
- objections and risks
- validated or invalidated value proposition statements
- MVP scope recommendations based on evidence

## Go / No-Go Criteria

Proceed to active implementation only when there is enough evidence that:

- at least one target segment has a strong repeated pain
- AURA's local offline-first nature matters to that segment
- users can describe daily or weekly use cases
- users trust the product direction enough to consider using it
- there is a plausible path to paid adoption

If evidence is weak, continue discovery or narrow the target segment before building.

## Repository Outputs

Validation work should produce:

- `docs/01_Product/value-proposition-validation.md`
- future interview summaries in `docs/01_Product/research/`
- updated PRD or MVP scope
- updated roadmap
- implementation tasks only after validation findings support them

## Technical Product Manager Rule

The Technical Product Manager must protect AURA from premature implementation.

The question is not only:

```text
Can we build it?
```

The question is:

```text
Should we build this now, for this user, because it moves us toward first paying customers?
```
