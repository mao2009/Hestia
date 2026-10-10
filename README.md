# Hestia

**An open-source, voice-enabled home automation assistant focused on flexible commands and proactive environmental optimization.**

Hestia translates natural-language requests into validated device and service actions. It also runs schedules and reacts to events to improve comfort, efficiency, and daily routines. It is **not** primarily a roleplay or general-companionship chatbot.

## Design goals

- Run on GPU-free, low-power Linux mini PCs (initial target: Intel N97 running Zorin OS).
- Use replaceable external LLM providers for intent interpretation and planning; do not require local LLM inference.
- Support voice and text command input, compound instructions, conditions, schedules, and follow-up corrections.
- Support proactive environmental optimization, with local rule execution even during LLM/API outages.
- Integrate with Home Assistant, MQTT, and optionally MCP-based tools.
- No built-in telemetry. No registration requirement for local operation.
- Keep credentials, household details, and sensor histories out of the source repository.
- Prefer proven, license-compatible OSS components over reimplementing infrastructure.

## Architecture at a glance

`Voice/Text -> Intent Adapter (LLM) -> Structured Action Plan -> Policy Validation -> Command Executor -> Integrations`

An independent `Scheduler/Event Monitor -> Optimization Planner -> Policy Validation -> Executor` pipeline handles automation. Risky, destructive, security-sensitive, or irreversible actions require stronger approval gates. **LLM responses are untrusted proposals, never direct device authority.**

## Planned development

1. Headless CLI/API prototype with a mock LLM adapter and simulated devices.
2. Real provider integration, structured commands, policy enforcement, and audit logs.
3. Voice input/output and hardware validation on N97/Zorin OS.
4. Scheduling, event handling, Home Assistant integration, and proactive optimization.
5. Optional Web UI and distributed low-cost voice satellites.

See [architecture](docs/ARCHITECTURE.md), [roadmap](docs/ROADMAP.md), and [security](docs/SECURITY.md) as they are added.

## Status

**Planning / pre-alpha.** The interface and implementation are not yet available. Hardware and latency claims require real-device benchmarks.

## Licensing

License selection is pending third-party dependency and distribution review. Apache-2.0 is the current candidate; no license grant should be inferred until a LICENSE file is added.

## Contributions

Issues and design feedback are welcome. Do not post API keys, private network layouts, audio recordings, or personal household data.
