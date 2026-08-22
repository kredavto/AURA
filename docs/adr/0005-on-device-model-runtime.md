# ADR-0005: On-Device Model Runtime

## Status

Accepted

## Context

The core AURA product promise depends on local LLM operation. The runtime must support mobile deployment, offline inference, predictable latency, and practical resource use.

## Decision

AURA will treat the on-device model runtime as a core system component.

Runtime selection must be documented per platform and evaluated against:

- offline execution
- supported model formats
- quantization support
- latency
- memory usage
- battery impact
- integration complexity
- licensing constraints

The MVP must avoid hard dependency on a single remote model provider.

## Consequences

- AI Model Router must support local model selection as the default path.
- Model packaging and update strategy must be explicit before implementation.
- Runtime benchmarks are required before alpha readiness.
- Cloud fallback, if introduced later, must be opt-in and privacy-reviewed.

## Related Documents

- `docs/03_AI/ai-model-router.md`
- `docs/03_AI/ai-architecture.md`
- `docs/04_Mobile/android-architecture.md`
- `docs/04_Mobile/ios-architecture.md`
