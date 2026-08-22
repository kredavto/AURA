# S0-005: Android Architecture

## Status

Accepted

## Purpose

This document defines the Android-specific architecture for AURA MVP.

It maps the accepted shared core and mobile client architecture to concrete Android implementation choices while keeping code implementation out of Sprint 0.

## Scope

This document covers:

- Android application structure
- recommended Kotlin and Jetpack stack
- module boundaries
- local data and secure storage choices
- local model runtime integration boundary
- STT and TTS integration boundary
- permissions
- offline behavior
- performance and validation expectations
- Claude Code implementation boundaries

This document does not define production source code, final UI design, final model selection, cloud services, payments, or release store operations.

## Product Context

AURA on Android must support an offline-first local assistant loop, local memory, text interaction, voice interaction, and user-controlled privacy settings.

The Android MVP should prioritize reliability, latency, privacy, battery behavior, and clear user control over breadth of features.

## Recommended Stack

| Area | Decision | Rationale |
| --- | --- | --- |
| Language | Kotlin | Native Android development, coroutine support, strong Jetpack ecosystem |
| UI | Jetpack Compose | Declarative UI, state-driven assistant screens, efficient iteration |
| Architecture | MVVM with unidirectional state flow | Predictable state handling for assistant, voice, memory, and errors |
| Async | Kotlin Coroutines and Flow | Streaming response state, STT/TTS state, local data observation |
| Local Database | Room over SQLite | Structured local conversation and memory metadata |
| Key-Value Settings | DataStore | Typed settings for privacy, memory, voice, diagnostics, model selection |
| Secure Storage | Android Keystore-backed encryption where needed | Protect sensitive keys and local encryption material |
| Dependency Injection | Hilt | Consistent scoped dependencies for app, session, repository, runtime boundaries |
| Background Work | WorkManager only for validated maintenance tasks | Avoid unnecessary background behavior in MVP |

## Android Module Model

Initial implementation should use a conservative modular structure:

```text
mobile/android/
  app/
  core/common/
  core/data/
  core/security/
  core/assistant/
  core/model-runtime/
  feature/assistant/
  feature/memory/
  feature/settings/
  feature/onboarding/
```

Module responsibilities:

| Module | Responsibility |
| --- | --- |
| `app` | Android entry point, navigation shell, dependency graph |
| `core/common` | Shared Kotlin utilities, result types, dispatchers, logging boundary |
| `core/data` | Room, DataStore, repositories, local data models |
| `core/security` | encryption, consent state, sensitive data handling |
| `core/assistant` | assistant session orchestration interfaces and state models |
| `core/model-runtime` | local model runtime wrapper and capability checks |
| `feature/assistant` | assistant screen, text input, voice controls, response rendering |
| `feature/memory` | memory list, edit, delete, disable, reset |
| `feature/settings` | privacy, voice, diagnostics, model/runtime settings |
| `feature/onboarding` | local-first explanation and permission education |

The first implementation may collapse modules if needed for speed, but boundaries must remain visible in packages and task scope.

## Application Layers

| Layer | Android Implementation |
| --- | --- |
| Presentation | Compose screens and reusable UI components |
| Interaction | ViewModels exposing immutable UI state and user intents |
| Assistant | Kotlin use cases for session lifecycle, prompt orchestration boundary, local model calls |
| Data | Room DAOs, repositories, DataStore settings |
| Runtime | Local model runtime adapter, STT adapter, TTS adapter |
| Security | Keystore-backed encryption and consent enforcement |

## Assistant State Flow

```text
Compose UI
  -> ViewModel intent
  -> Assistant use case
  -> consent and safety checks
  -> local memory repository
  -> prompt orchestration interface
  -> local model runtime adapter
  -> streaming or chunked response state
  -> conversation repository
  -> Compose UI render
```

The flow must remain functional with network disabled.

## Local Data Architecture

### Room Entities

Initial data model should include:

| Entity | Purpose |
| --- | --- |
| `ConversationEntity` | Local conversation metadata |
| `MessageEntity` | User and assistant messages when history is enabled |
| `MemoryEntity` | User-approved memory item or summary |
| `MemoryEmbeddingEntity` | Local embedding reference or vector storage strategy |
| `DiagnosticEventEntity` | Non-sensitive local diagnostic event |

Room schema must avoid storing voice recordings by default.

### DataStore Settings

DataStore should store:

- history enabled
- memory enabled
- voice input enabled
- voice output enabled
- diagnostics enabled
- selected local model profile
- onboarding completion

### Sensitive Data Rule

Messages, memories, embeddings, and generated summaries are private user data. They must not be written to logs, crash reports, analytics, or remote endpoints by default.

## Security Architecture Boundary

Android implementation must support:

- local-only default operation
- explicit consent before memory use
- full local memory reset
- conversation history toggle
- sensitive logging disabled by default
- encryption strategy for sensitive local data
- secure handling of model/runtime configuration

Security details must be finalized in `docs/05_Security/security-architecture.md` before implementation tasks modify data handling.

## Model Runtime Boundary

The Android app must integrate local model execution through a runtime adapter:

```text
interface LocalModelRuntime {
  fun capabilities(): ModelCapabilities
  fun generate(request: ModelRequest): Flow<ModelToken>
  fun cancel(sessionId: String)
}
```

Runtime implementation may later use a mobile-compatible local inference backend, but Sprint 0 does not select a final backend.

Selection criteria:

- offline execution
- acceptable latency on target devices
- memory and thermal behavior
- quantized model support
- streaming or incremental output support
- license compatibility
- app package and model distribution feasibility

## STT Boundary

Android STT must be abstracted behind an adapter:

```text
interface SpeechToTextEngine {
  fun startListening(config: SttConfig): Flow<SttEvent>
  fun stopListening()
  fun isAvailable(): Boolean
}
```

MVP behavior:

- request microphone permission at point of need
- allow cancel and retry
- allow user correction before assistant generation
- avoid persisting raw audio by default
- degrade to text-only mode when STT is unavailable

## TTS Boundary

Android TTS must be abstracted behind an adapter:

```text
interface TextToSpeechEngine {
  fun speak(text: String, config: TtsConfig): Flow<TtsEvent>
  fun stop()
  fun isAvailable(): Boolean
}
```

MVP behavior:

- TTS is optional per user setting
- stop control must be visible during playback
- app must remain usable in text-only mode
- generated speech audio is not persisted by default

## Permissions

| Permission | Use | MVP Rule |
| --- | --- | --- |
| Microphone | Voice input | Request only when user starts voice input |
| Notifications | Future reminders or background updates | Out of scope unless value validation requires it |
| Network | Optional future diagnostics or model download | Core MVP must work without requiring it |
| Storage | Model files or local export where needed | Use scoped storage and least privilege |

The Android MVP must not require account login or cloud permissions.

## Offline Behavior

Android MVP must pass these offline cases:

- launch in airplane mode
- open assistant screen
- send text prompt
- retrieve local memory when enabled
- generate local response
- save local conversation when history is enabled
- open memory screen
- edit or delete local memory
- use text-only fallback when voice runtime is unavailable

## Performance Targets

Initial targets should be refined through benchmarking, but Android implementation should optimize for:

- app launch without model initialization blocking the UI
- visible assistant progress state within one second after submit
- cancellable model generation
- bounded memory usage on mid-range devices
- thermal and battery safeguards for long generations
- graceful handling when selected model cannot run

## Error Handling

Android UI must distinguish:

- permission required
- local model unavailable
- device resource limit
- STT unavailable
- TTS unavailable
- storage failure
- generation canceled
- recoverable runtime error

Error states should provide retry, cancel, settings, or text-only fallback where applicable.

## Claude Code Boundaries

Claude Code implementation tasks for Android must:

- reference this document and relevant ADRs
- specify target module and package
- avoid adding cloud dependencies unless explicitly approved
- avoid storing private user content in logs
- include local/offline validation steps
- include tests for ViewModel state and local data behavior where applicable

## MVP Exclusions

Android MVP excludes:

- cloud account requirement
- multi-device sync
- background autonomous actions
- notification-driven assistant behavior
- payment flow
- enterprise management
- plugin marketplace
- remote telemetry containing personal content

## Validation Approach

This architecture is valid when:

- it maps all shared core modules to Android components
- Android can support offline text assistant flow
- voice path has clear STT/TTS adapter boundaries
- local memory can be inspected and deleted by the user
- security architecture can define concrete data protections
- Claude Code can implement Android skeleton tasks without making architecture decisions

## Related ADRs

- `docs/adr/0001-local-first-mobile-llm.md`
- `docs/adr/0002-offline-first-operation.md`
- `docs/adr/0003-local-memory-first.md`
- `docs/adr/0004-mobile-platform-split.md`
- `docs/adr/0005-on-device-model-runtime.md`
- `docs/adr/0006-voice-first-interface.md`
- `docs/adr/0007-security-and-privacy-boundary.md`
- `docs/adr/0010-claude-code-implementation-boundary.md`

## Related Documents

- `docs/02_Architecture/shared-core-architecture.md`
- `docs/04_Mobile/mobile-client-architecture.md`
- `docs/04_Mobile/ios-architecture.md`
- `docs/03_AI/ai-model-router.md`
- `docs/03_AI/stt-engine.md`
- `docs/03_AI/tts-engine.md`
- `docs/05_Security/security-architecture.md`
