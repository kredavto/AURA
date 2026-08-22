# S0-006: iOS Architecture

## Status

Accepted

## Purpose

This document defines the iOS-specific architecture for AURA MVP.

It maps the accepted shared core and mobile client architecture to concrete iOS implementation choices while keeping code implementation out of Sprint 0.

## Scope

This document covers:

- iOS application structure
- recommended Swift and Apple platform stack
- module boundaries
- local data and secure storage choices
- local model runtime integration boundary
- STT and TTS integration boundary
- permissions
- offline behavior
- performance and validation expectations
- Claude Code implementation boundaries

This document does not define production source code, final UI design, final model selection, cloud services, payments, or App Store release operations.

## Product Context

AURA on iOS must support an offline-first local assistant loop, local memory, text interaction, voice interaction, and user-controlled privacy settings.

The iOS MVP should prioritize reliability, local privacy, battery behavior, responsive UI, and clear user control over broad feature count.

## Recommended Stack

| Area | Decision | Rationale |
| --- | --- | --- |
| Language | Swift | Native iOS development, strong Apple ecosystem support |
| UI | SwiftUI | Declarative UI, state-driven assistant screens, efficient iteration |
| Architecture | MVVM with explicit state models | Predictable assistant, voice, memory, and settings behavior |
| Async | Swift Concurrency and AsyncSequence | Streaming response state, STT/TTS state, local runtime operations |
| Local Database | SQLite-backed persistence through a stable local persistence layer | Structured local conversation and memory metadata |
| Key-Value Settings | UserDefaults or app settings store wrapper | Lightweight typed settings for MVP preferences |
| Secure Storage | Keychain and file protection where needed | Protect sensitive keys and local encryption material |
| Audio | AVFoundation boundary | Microphone, playback, session configuration |
| Speech | Speech framework or local STT runtime adapter where available | Platform speech integration behind project interface |

Final persistence and model runtime choices must be validated before implementation tasks begin.

## iOS Module Model

Initial implementation should use a conservative modular structure:

```text
mobile/ios/
  AuraApp/
  Core/Common/
  Core/Data/
  Core/Security/
  Core/Assistant/
  Core/ModelRuntime/
  Feature/Assistant/
  Feature/Memory/
  Feature/Settings/
  Feature/Onboarding/
```

Module responsibilities:

| Module | Responsibility |
| --- | --- |
| `AuraApp` | iOS entry point, navigation shell, dependency composition |
| `Core/Common` | shared Swift utilities, result types, logging boundary |
| `Core/Data` | local persistence, repositories, settings store |
| `Core/Security` | Keychain access, file protection, consent state, sensitive data handling |
| `Core/Assistant` | assistant session orchestration interfaces and state models |
| `Core/ModelRuntime` | local model runtime wrapper and capability checks |
| `Feature/Assistant` | assistant screen, text input, voice controls, response rendering |
| `Feature/Memory` | memory list, edit, delete, disable, reset |
| `Feature/Settings` | privacy, voice, diagnostics, model/runtime settings |
| `Feature/Onboarding` | local-first explanation and permission education |

The first implementation may collapse modules if needed for speed, but boundaries must remain visible in folders, types, and task scope.

## Application Layers

| Layer | iOS Implementation |
| --- | --- |
| Presentation | SwiftUI views and reusable components |
| Interaction | Observable view models exposing immutable UI state and user intents |
| Assistant | Swift use cases for session lifecycle, prompt orchestration boundary, local model calls |
| Data | repositories, persistence adapters, settings store |
| Runtime | local model runtime adapter, STT adapter, TTS adapter |
| Security | Keychain, file protection, consent enforcement |

## Assistant State Flow

```text
SwiftUI View
  -> ViewModel intent
  -> Assistant use case
  -> consent and safety checks
  -> local memory repository
  -> prompt orchestration interface
  -> local model runtime adapter
  -> streaming or chunked response state
  -> conversation repository
  -> SwiftUI render
```

The flow must remain functional with network disabled.

## Local Data Architecture

### Initial Entities

Initial data model should include:

| Entity | Purpose |
| --- | --- |
| `ConversationRecord` | Local conversation metadata |
| `MessageRecord` | User and assistant messages when history is enabled |
| `MemoryRecord` | User-approved memory item or summary |
| `MemoryEmbeddingRecord` | Local embedding reference or vector storage strategy |
| `DiagnosticEventRecord` | Non-sensitive local diagnostic event |

The local persistence layer must avoid storing voice recordings by default.

### Settings

The settings store should include:

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

iOS implementation must support:

- local-only default operation
- explicit consent before memory use
- full local memory reset
- conversation history toggle
- sensitive logging disabled by default
- file protection for local private data
- Keychain-backed protection for sensitive keys or encryption material
- secure handling of model/runtime configuration

Security details must be finalized in `docs/05_Security/security-architecture.md` before implementation tasks modify data handling.

## Model Runtime Boundary

The iOS app must integrate local model execution through a runtime adapter:

```text
protocol LocalModelRuntime {
  func capabilities() async -> ModelCapabilities
  func generate(_ request: ModelRequest) -> AsyncThrowingStream<ModelToken, Error>
  func cancel(sessionId: String)
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
- compatibility with Apple platform review constraints

## STT Boundary

iOS STT must be abstracted behind an adapter:

```text
protocol SpeechToTextEngine {
  func startListening(config: SttConfig) -> AsyncThrowingStream<SttEvent, Error>
  func stopListening()
  func isAvailable() async -> Bool
}
```

MVP behavior:

- request microphone and speech recognition permissions at point of need
- allow cancel and retry
- allow user correction before assistant generation
- avoid persisting raw audio by default
- degrade to text-only mode when STT is unavailable

## TTS Boundary

iOS TTS must be abstracted behind an adapter:

```text
protocol TextToSpeechEngine {
  func speak(_ text: String, config: TtsConfig) -> AsyncThrowingStream<TtsEvent, Error>
  func stop()
  func isAvailable() async -> Bool
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
| Speech Recognition | STT where platform speech services are used | Request only when user starts voice input |
| Notifications | Future reminders or background updates | Out of scope unless value validation requires it |
| Network | Optional future diagnostics or model download | Core MVP must work without requiring it |
| Files | User export/import where needed | Use least privilege and explicit user action |

The iOS MVP must not require account login or cloud permissions.

## Offline Behavior

iOS MVP must pass these offline cases:

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

Initial targets should be refined through benchmarking, but iOS implementation should optimize for:

- app launch without model initialization blocking the UI
- visible assistant progress state within one second after submit
- cancellable model generation
- bounded memory usage on supported devices
- thermal and battery safeguards for long generations
- graceful handling when selected model cannot run
- predictable behavior across foreground and interrupted audio sessions

## Error Handling

iOS UI must distinguish:

- microphone permission required
- speech recognition permission required
- local model unavailable
- device resource limit
- STT unavailable
- TTS unavailable
- storage failure
- generation canceled
- recoverable runtime error

Error states should provide retry, cancel, settings, or text-only fallback where applicable.

## Claude Code Boundaries

Claude Code implementation tasks for iOS must:

- reference this document and relevant ADRs
- specify target module and folder
- avoid adding cloud dependencies unless explicitly approved
- avoid storing private user content in logs
- include local/offline validation steps
- include tests for view model state and local data behavior where applicable

## MVP Exclusions

iOS MVP excludes:

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

- it maps all shared core modules to iOS components
- iOS can support offline text assistant flow
- voice path has clear STT/TTS adapter boundaries
- local memory can be inspected and deleted by the user
- security architecture can define concrete data protections
- Claude Code can implement iOS skeleton tasks without making architecture decisions

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
- `docs/04_Mobile/android-architecture.md`
- `docs/03_AI/ai-model-router.md`
- `docs/03_AI/stt-engine.md`
- `docs/03_AI/tts-engine.md`
- `docs/05_Security/security-architecture.md`
