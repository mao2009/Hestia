# Roadmap (Draft)

## M0 — Foundation
- .NET solution, module boundaries, CI, formatting and tests.
- Configuration, secrets strategy, logging, provider abstraction.
- CLI-driven simulated device proof-of-concept.

**Gate:** clean build and reproducible automated tests without API keys or hardware.

## M1 — Reliable natural-language control
- Typed commands, structured planner, compound operations and follow-up references.
- Policy enforcement, confirmations, dry runs, rate limits and audit.
- External LLM integration behind replaceable provider interface.

**Gate:** evaluate Japanese command fixtures, ambiguous requests, prompt injection and partial failures.

## M2 — Voice on N97
- Wake-word, VAD, Japanese STT, brief TTS, microphone mute.
- Measure idle CPU/RAM/power and speech-to-action latency on Zorin OS.
- Avoid unnecessary audio retention or transmission.

**Gate:** repeatable end-to-end voice scenarios on physical N97.

## M3 — Automation and integrations
- Durable schedules, conditional triggers and event ingestion.
- Home Assistant + MQTT adapters; optional MCP adapters.
- Offline deterministic automation and safe recovery after reboot.

**Gate:** scheduled actions survive restart without duplicate execution.

## M4 — Proactive optimization
- Observe environmental measurements and approved preferences.
- Recommend interventions before permitting bounded automation.
- Explain actions, provide override/pause/undo where feasible.
- Track comfort/energy metrics without storing unnecessary personal data.

**Gate:** simulations demonstrate no unsafe action or uncontrolled API-cost growth.

## Later
- Browser administration, ESP32 voice satellite protocol, packaging and updates.

No release dates or completion percentages are claimed until implementation and measurements exist.
