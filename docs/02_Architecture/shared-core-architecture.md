# S0-013: Shared Core Architecture

## Status

Accepted

## Purpose

This document defines the shared architecture core for AURA before platform-specific Android, iOS, AI, memory, speech, and security documents are expanded.

It exists to prevent duplicated architecture decisions across mobile platforms and to keep the MVP implementation focused.

## Scope

This document covers:

- shared product capabilities
- core module boundaries
- local-first execution model
- data ownership boundaries
- platform integration boundaries
- implementation constraints for Claude Code

This document does not define Android-specific APIs, iOS-specific APIs, final model runtime selection, UI design details, or production source code.

## Product Context

AURA is a commercial offline-first local LLM assistant for mobile devices.

The MVP must support daily assistant use, local personal context, local memory, text interaction, and voice interaction without making cloud services mandatory.

## Architecture Principles

1. Local-first execution is the default.
2. Offline operation is a required product behavior.
3. User private data stays on device by default.
4. Shared architecture defines concepts; platforms define execution details.
5. MVP scope must remain narrow enough to validate commercial demand.
6. Claude Code must implement from repository artifacts, not private chat context.

## Shared Core Modules

| Module | Responsibility | MVP Requirement |
| --- | --- | --- |
| Assistant Session | Owns a user interaction session and response lifecycle | Required |
| Conversation Store | Stores local conversation history where enabled | Required |
| Memory Engine Interface | Provides controlled access to local user memory | Required |
| Model Router Interface | Selects local model/runtime path | Required |
| Prompt Orchestrator | Builds prompts from user input, memory, and system constraints | Required |
| Safety And Policy Guard | Applies local safety, consent, and privacy constraints | Required |
| STT Interface | Converts speech to text through platform/runtime implementation | Required for voice path |
| TTS Interface | Converts assistant response to speech through platform/runtime implementation | Required for voice path |
| Settings And Consent | Stores user choices for memory, voice, privacy, and diagnostics | Required |
| Diagnostics Interface | Captures non-sensitive technical diagnostics | Limited |

## Core Runtime Flow

```text
User input
  -> Input Controller
  -> STT Interface when voice input is used
  -> Assistant Session
  -> Safety And Policy Guard
  -> Memory Engine Interface
  -> Prompt Orchestrator
  -> Model Router Interface
  -> Local Model Runtime
  -> Assistant Session
  -> Conversation Store
  -> TTS Interface when voice output is enabled
  -> User output
```

The flow must work without network access.

## Data Ownership

| Data Class | Default Location | Rule |
| --- | --- | --- |
| User messages | Local device | Stored only if history is enabled |
| Assistant responses | Local device | Stored only if history is enabled |
| Memories | Local device | User can view, edit, delete, and disable |
| Embeddings | Local device | Treated as private derived user data |
| Voice input | Local transient processing | Persist only with explicit product decision |
| Voice output | Local transient processing | Persist only with explicit product decision |
| Diagnostics | Local or optional export | Must not include raw personal content |

## Platform Boundary

Shared core defines interfaces and behavior. Android and iOS documents must define:

- local model runtime integration
- storage implementation
- secure storage implementation
- background execution limits
- speech API/runtime choices
- permissions
- packaging constraints
- performance targets

Shared core must not assume identical runtime capabilities across Android and iOS.

## MVP Constraints

The MVP must include:

- local text assistant loop
- local memory interface
- local model routing interface
- user-controlled memory behavior
- local conversation history setting
- voice input and output architecture
- offline-mode validation path

The MVP must not require:

- cloud inference
- cloud memory
- multi-device sync
- enterprise administration
- plugin marketplace
- autonomous external actions
- payment implementation before value validation

## Alternatives Considered

### Single Cross-Platform App Core

Rejected for now because model runtime, speech, secure storage, and background behavior differ materially across Android and iOS.

### Cloud-First Assistant Core

Rejected for MVP because it conflicts with the offline-first and local privacy product direction.

### Platform-Only Architecture Without Shared Core

Rejected because it would duplicate product and AI decisions across Android and iOS and increase documentation drift.

## Consequences

- Android and iOS architecture can diverge where platform constraints require it.
- AI, memory, STT, TTS, and security documents must align to the shared module boundaries.
- Claude Code tasks must specify whether work touches shared concepts, Android, iOS, AI, or security boundaries.
- Scope expansion requires updating the relevant ADR or architecture document first.

## Validation Approach

Shared core is valid when:

- Android architecture can map each shared module to concrete platform components.
- iOS architecture can map each shared module to concrete platform components.
- AI architecture can implement model routing and prompt orchestration without inventing new top-level modules.
- Security architecture can classify all shared data classes.
- Claude Code can prepare implementation tasks without needing private chat context.

## Related ADRs

- `docs/adr/0001-local-first-mobile-llm.md`
- `docs/adr/0002-offline-first-operation.md`
- `docs/adr/0003-local-memory-first.md`
- `docs/adr/0004-mobile-platform-split.md`
- `docs/adr/0005-on-device-model-runtime.md`
- `docs/adr/0006-voice-first-interface.md`
- `docs/adr/0007-security-and-privacy-boundary.md`
- `docs/adr/0008-value-proposition-before-code.md`
- `docs/adr/0010-claude-code-implementation-boundary.md`

## Related Documents

- `docs/00_Project/aura-spec.md`
- `docs/00_Project/master-index.md`
- `docs/04_Mobile/mobile-client-architecture.md`
- `docs/03_AI/ai-architecture.md`
- `docs/05_Security/security-architecture.md`
