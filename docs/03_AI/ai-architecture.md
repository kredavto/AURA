# S0-011: AI Architecture

## Status

Accepted

## Purpose

This document defines the AI architecture for AURA MVP.

It turns the accepted local-first product direction into a concrete assistant architecture that can guide Memory Engine, STT Engine, TTS Engine, AI Model Router, mobile implementation tasks, and future evaluation work.

## Scope

This document covers:

- assistant loop
- prompt orchestration
- model runtime boundary
- memory boundary
- safety and privacy guard
- offline behavior
- evaluation strategy
- implementation boundaries for Claude Code

This document does not select a final model, implement runtime code, define exact prompts, train models, define cloud fallback, or implement memory storage.

## Product Context

AURA is a commercial offline-first local LLM assistant for mobile devices.

The AI system must make the product useful as a daily assistant and personal knowledge base while keeping private user data local by default.

## Core AI Principles

1. Local inference is the default path.
2. Offline operation is a required behavior, not a fallback edge case.
3. Memory must be user-controlled and inspectable.
4. The assistant must be useful without hidden cloud dependencies.
5. Prompt orchestration must be deterministic enough to test.
6. Safety and privacy constraints must run before and after model generation.
7. The MVP must avoid autonomous external actions.

## AI System Components

| Component | Responsibility | MVP Status |
| --- | --- | --- |
| Assistant Session | Owns one user interaction lifecycle | Required |
| Input Normalizer | Converts text or STT output into a normalized user request | Required |
| Safety And Privacy Guard | Applies consent, data-use, and response constraints | Required |
| Memory Context Builder | Retrieves approved local memory context | Required |
| Prompt Orchestrator | Builds model-ready prompt from instruction, user input, memory, and constraints | Required |
| AI Model Router | Selects local model profile and runtime adapter | Required |
| Local Model Runtime | Executes on-device inference through platform adapter | Required |
| Response Post-Processor | Applies formatting, privacy, and safety checks after generation | Required |
| Evaluation Harness | Tests behavior, latency, privacy, and offline operation | Required before alpha |

## Assistant Runtime Flow

```text
User input
  -> Input Normalizer
  -> Safety And Privacy Guard
  -> Memory Context Builder
  -> Prompt Orchestrator
  -> AI Model Router
  -> Local Model Runtime
  -> Response Post-Processor
  -> Assistant Session
  -> Mobile Client Output
```

For voice input, STT runs before Input Normalizer.

For voice output, TTS runs after Response Post-Processor and user-visible response creation.

## Assistant Session

Assistant Session is responsible for:

- session id
- user input state
- cancellation
- retry
- streaming or incremental output state
- memory usage decision
- final response state
- error state
- diagnostics boundary

Assistant Session must not directly own platform storage or runtime implementation. It must depend on interfaces.

## Prompt Orchestration

Prompt Orchestrator builds the final model request from:

- system instruction
- product behavior constraints
- user input
- selected conversation context
- approved memory context
- safety and privacy constraints
- model profile constraints

Prompt construction must be traceable and testable.

The MVP should use a small number of prompt templates:

| Template | Purpose |
| --- | --- |
| `general-assistant` | Default daily assistant response |
| `memory-aware-assistant` | Assistant response using approved memory context |
| `memory-write-candidate` | Candidate extraction for possible memory updates |
| `clarification` | Ask a clarifying question when user intent is underspecified |
| `offline-limitation` | Explain local/offline limitations without exposing internal details |

Exact prompt text should be stored later in `docs/03_AI/prompts/` or equivalent if prompt governance expands.

## Memory Boundary

AI Architecture defines how memory is used; Memory Engine defines how memory is stored, retrieved, updated, and deleted.

The AI layer may request:

- relevant memories for a user request
- candidate memory extraction from a conversation
- memory disablement status
- memory deletion or reset status

The AI layer must not silently store memory without a user-approved Memory Engine policy.

## Model Runtime Boundary

The AI layer calls model execution through a runtime interface:

```text
ModelRequest
  -> model profile
  -> prompt
  -> generation parameters
  -> privacy constraints
  -> cancellation token
```

```text
ModelResponse
  -> tokens or chunks
  -> final text
  -> runtime metadata
  -> error state
```

The runtime must support:

- offline execution
- cancellation
- bounded resource use
- runtime availability checks
- graceful unsupported-device behavior

Final model/runtime selection belongs to AI Model Router and platform architecture.

## Safety And Privacy Guard

The guard must run at these points:

1. before memory retrieval
2. before prompt construction
3. before model generation
4. after model generation

MVP responsibilities:

- enforce memory enabled/disabled state
- prevent raw private data from diagnostics
- prevent hidden remote transmission
- handle unsupported requests without pretending to have capabilities
- avoid autonomous external actions
- preserve user control over memory and conversation state

## Offline Behavior

The AI system must handle offline mode as normal operation.

Required offline behavior:

- answer using local model when available
- retrieve local memory when enabled
- avoid remote dependency errors in the main assistant flow
- explain unavailable network-dependent capabilities plainly
- preserve cancellation and retry
- produce diagnostics without raw personal content

## Evaluation Strategy

Evaluation must cover:

| Category | What To Validate |
| --- | --- |
| Offline operation | Assistant works with network unavailable |
| Latency | User sees progress quickly and can cancel |
| Memory use | Memory is used only when enabled and relevant |
| Privacy | Raw user content is not logged or transmitted |
| Helpfulness | Responses solve common daily assistant tasks |
| Grounding | Assistant does not claim unavailable device or cloud capabilities |
| Voice integration | STT/TTS boundaries do not alter assistant safety rules |
| Resource behavior | Model failure or unsupported device state is graceful |

Evaluation fixtures should later include:

- user prompt
- memory state
- settings state
- expected assistant behavior
- unacceptable behavior
- offline requirement

## MVP AI Capabilities

Required:

- local text assistant response
- memory-aware response when memory is enabled
- memory-disabled response path
- clarification when request is underspecified
- local runtime unavailable handling
- cancellable generation
- text-only fallback for voice failures

Deferred:

- cloud fallback
- tool use
- autonomous actions
- web browsing
- multi-step agent planning
- multi-device memory
- paid feature gating
- model training

## Claude Code Boundaries

Claude Code implementation tasks touching AI must:

- reference this document and relevant ADRs
- specify whether the task affects session, prompt, memory, router, runtime, STT, TTS, or evaluation
- avoid adding remote model dependencies unless explicitly approved
- avoid storing private content in logs or tests
- include offline validation
- include behavior tests for key assistant states

If implementation exposes a missing architecture decision, create or update the relevant document before continuing.

## Validation Approach

This architecture is valid when:

- Memory Engine can implement the memory boundary without redefining assistant flow.
- AI Model Router can implement local model selection without redefining session flow.
- STT and TTS can attach before and after the assistant loop without bypassing safety rules.
- Android and iOS can call the same conceptual AI interfaces through platform adapters.
- Security Architecture can classify every AI data path.
- Claude Code can prepare implementation tasks from repository context alone.

## Related ADRs

- `docs/adr/0001-local-first-mobile-llm.md`
- `docs/adr/0002-offline-first-operation.md`
- `docs/adr/0003-local-memory-first.md`
- `docs/adr/0005-on-device-model-runtime.md`
- `docs/adr/0006-voice-first-interface.md`
- `docs/adr/0007-security-and-privacy-boundary.md`
- `docs/adr/0008-value-proposition-before-code.md`
- `docs/adr/0010-claude-code-implementation-boundary.md`

## Related Documents

- `docs/02_Architecture/shared-core-architecture.md`
- `docs/03_AI/memory-engine.md`
- `docs/03_AI/stt-engine.md`
- `docs/03_AI/tts-engine.md`
- `docs/03_AI/ai-model-router.md`
- `docs/04_Mobile/mobile-client-architecture.md`
- `docs/05_Security/security-architecture.md`
