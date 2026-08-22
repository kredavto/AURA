# S0-004: Mobile Client Architecture

## Status

Accepted

## Purpose

This document defines the cross-platform mobile client architecture for AURA.

It translates the accepted shared core into a user-facing mobile application structure while leaving Android and iOS implementation details to platform-specific documents.

## Scope

This document covers:

- mobile application layers
- user interaction flows
- local assistant session behavior
- memory and conversation access from the mobile client
- voice and text paths
- settings and consent surfaces
- offline behavior
- boundaries for Android and iOS implementation

This document does not define platform APIs, final UI screens, production source code, model runtime internals, or legal copy.

## Product Context

AURA is a commercial offline-first local LLM assistant for mobile devices.

The mobile client must make the product useful for daily use while preserving the local-first privacy model. The MVP should prioritize a reliable assistant loop over broad feature count.

## Client Layers

| Layer | Responsibility | Notes |
| --- | --- | --- |
| Presentation Layer | Screens, input controls, voice controls, response rendering | Platform-specific implementation |
| Interaction Layer | User intents, session commands, cancellation, retry, correction | Shared behavior, platform-specific wiring |
| Assistant Layer | Assistant session lifecycle and response orchestration | Aligned with shared core |
| Memory Access Layer | User-approved memory read/write/delete operations | Must expose user control |
| Local Data Layer | Conversation, memory, settings, diagnostics storage | Platform-specific storage |
| Runtime Integration Layer | Model, STT, TTS, and performance integration | Platform-specific implementation |
| Security And Consent Layer | Permissions, privacy controls, local data rules | Must align with security architecture |

## Primary MVP Flows

### Text Assistant Flow

```text
User opens AURA
  -> enters text
  -> assistant session starts
  -> local memory context is retrieved if enabled
  -> local model response is generated
  -> response is displayed
  -> conversation is stored if history is enabled
```

### Voice Assistant Flow

```text
User starts voice input
  -> microphone permission is checked
  -> STT produces text
  -> user can confirm, cancel, or correct
  -> assistant session runs text assistant flow
  -> TTS speaks response if enabled
```

### Memory Control Flow

```text
User opens memory controls
  -> views remembered items or summaries
  -> edits, deletes, disables, or resets memory
  -> changes take effect locally
```

### Offline Flow

```text
Device has no network
  -> app remains usable
  -> local assistant session runs
  -> local memory remains accessible
  -> network-dependent optional features are hidden or marked unavailable
```

## MVP Screens

| Screen | Purpose | MVP Status |
| --- | --- | --- |
| Assistant | Main text and voice assistant interaction | Required |
| Conversation History | Local previous conversations if enabled | Required |
| Memory | View, edit, delete, disable, and reset memory | Required |
| Settings | Privacy, voice, model, memory, and diagnostics controls | Required |
| Onboarding | Explain local-first behavior and request permissions | Required |
| Diagnostics | Show non-sensitive technical status | Limited |

The first screen after onboarding should be the assistant, not a marketing page.

## State Model

| State | Description |
| --- | --- |
| Idle | Ready for text or voice input |
| Listening | Capturing voice input |
| Transcribing | Converting voice to text |
| Confirming Input | Allowing user correction before assistant response |
| Thinking | Running local model response generation |
| Speaking | Playing TTS response |
| Offline Ready | Network unavailable but local flow functional |
| Permission Needed | User action required for microphone or local capability |
| Resource Limited | Device cannot run selected model or voice path reliably |
| Error Recoverable | User can retry, cancel, or switch input mode |

## Local Data Rules

- Conversation history is local and user-controlled.
- Memory is local and must be inspectable and deletable.
- Voice input should be transient unless a future reviewed decision allows persistence.
- Diagnostics must not include raw personal content.
- Export and reset behavior must be planned before alpha readiness.

## Permissions

The mobile client may request:

- microphone permission for voice input
- local file/storage access only when required by platform implementation
- notification permission only if a validated MVP use case requires it

Permissions must be requested at the point of need with clear user value.

## Offline Requirements

The mobile client must:

- launch without network access
- complete a text assistant session without network access
- access local memory without network access
- show clear local model/runtime status
- avoid blocking the main assistant screen on remote services

## Performance Requirements

Initial MVP targets must be defined per platform, but the mobile client should optimize for:

- fast app launch
- responsive input field
- visible response progress
- cancellable generation
- bounded memory usage
- battery-aware voice and inference behavior

## Android And iOS Boundaries

Android architecture must define:

- Kotlin/Jetpack structure
- storage APIs
- model runtime integration
- STT/TTS implementation choices
- permissions and background limits

iOS architecture must define:

- Swift/SwiftUI structure
- storage APIs
- model runtime integration
- STT/TTS implementation choices
- permissions and background limits

Both platform documents must map back to this mobile client architecture and the shared core architecture.

## MVP Exclusions

The mobile client MVP excludes:

- multi-device sync
- cloud account requirement
- plugin ecosystem
- autonomous external actions
- social features
- enterprise administration
- payment flow before value proposition validation

## Validation Approach

The mobile client architecture is valid when:

- it supports offline text assistant use
- it supports voice input and output architecture
- it exposes memory control to the user
- Android and iOS documents can implement it without inventing new product flows
- security architecture can classify every local data surface
- Claude Code can receive implementation tasks with clear scope

## Related ADRs

- `docs/adr/0001-local-first-mobile-llm.md`
- `docs/adr/0002-offline-first-operation.md`
- `docs/adr/0003-local-memory-first.md`
- `docs/adr/0004-mobile-platform-split.md`
- `docs/adr/0006-voice-first-interface.md`
- `docs/adr/0007-security-and-privacy-boundary.md`
- `docs/adr/0008-value-proposition-before-code.md`

## Related Documents

- `docs/02_Architecture/shared-core-architecture.md`
- `docs/04_Mobile/android-architecture.md`
- `docs/04_Mobile/ios-architecture.md`
- `docs/03_AI/ai-architecture.md`
- `docs/03_AI/stt-engine.md`
- `docs/03_AI/tts-engine.md`
- `docs/05_Security/security-architecture.md`
