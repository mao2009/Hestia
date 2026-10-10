# Roadmap (Draft)

## Design selection gate (before large implementation)
- Inventory reusable OSS, focusing on Home Assistant, MQTT, voice stack and dashboard options.
- Decide what Hestia owns vs delegates; compare self-contained and Home Assistant-backed modes.
- Record dependency licenses, interoperability and N97 CPU/RAM impact.
- Preserve voice / Web UI / API as first-class interfaces to one command and policy engine.
- See #16.

**Gate:** documented trade-offs, bounded initial scope, and no unverified performance claims.

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

## M1b — Local administration Web UI
- Host an authenticated, responsive local Web UI on the N97 device.
- Show devices, status and configuration with server-enforced permissions.
- Keep default listening interface LAN/local-only and avoid telemetry.
- See #13.

**Gate:** safe login, settings management and access-denial tests.

## M1c — Skills SDK
- Specify versioned manifests and typed interfaces for commands, events, automations and integration-specific configuration.
- Prove core runtime and shared policy boundary with an isolated mock skill.
- See #22.

**Gate:** installable mock skills cannot obtain undeclared permissions.

## M2c — Secure skill runtime and management
- Add controlled skill lifecycle, isolated execution, permissions, resource limits, compatibility checks and upgrades/rollback.
- Add Web UI skill catalog, configuration, explicit permission grants and health checks.
- See #23–#24.

**Gate:** security regression tests and reliable recovery after a skill crash or upgrade.

## M2 — Voice on N97
- Wake-word, VAD, Japanese STT, brief TTS, microphone mute.
- Measure idle CPU/RAM/power and speech-to-action latency on Zorin OS.
- Avoid unnecessary audio retention or transmission.

**Gate:** repeatable end-to-end voice scenarios on physical N97.

## M2b — Monitoring dashboard
- Present command and device status, errors, API budgets, and system health.
- Store only necessary local metrics with retention and deletion controls.
- See #14.

**Gate:** dashboard handles offline and missing data honestly and remains lightweight on N97.

## M3 — Automation and integrations
- Durable schedules, conditional triggers and event ingestion.
- Home Assistant + MQTT adapters; optional MCP adapters.
- Offline deterministic automation and safe recovery after reboot.

**Gate:** scheduled actions survive restart without duplicate execution.

## M3a — Google ecosystem and unified notifications
- Integrate account connection/permissions, Gmail, Google Calendar, Google Tasks and selective Google Drive operations.
- Add unified opt-in notifications for calendar/email/device events and optional Amazon shipment emails; retain Alexa in parallel during migration.
- Expose services in Web UI and voice interface using the shared policy engine.
- See #17–#21.

**Gate:** integration tests for revocation, permissions, accidental disclosure, duplicate alerts and consequential-write confirmations.

## M3b — Visual automation management
- Create, inspect, simulate, pause and audit schedules and conditional rules.
- Expose policy management and emergency pause in the authenticated Web UI.
- See #15.

**Gate:** every Web UI action is checked by the same policy engine as voice/CLI actions.

## M4 — Proactive optimization
- Observe environmental measurements and approved preferences.
- Recommend interventions before permitting bounded automation.
- Explain actions, provide override/pause/undo where feasible.
- Track comfort/energy metrics without storing unnecessary personal data.

**Gate:** simulations demonstrate no unsafe action or uncontrolled API-cost growth.

## Later
- ESP32 voice satellite protocol, packaging and updates.

No release dates or completion percentages are claimed until implementation and measurements exist.
