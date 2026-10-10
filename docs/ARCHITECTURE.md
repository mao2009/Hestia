# Architecture (Draft)

## Constraints
- Intel N97 mini PC / Zorin OS Linux as first validation target; no dedicated GPU.
- A replaceable external LLM API may be used; voice recognition/synthesis may be local or API-based.
- Core command and automation logic must work headlessly without microphones.
- Default-deny for actions not registered or authorized.

## Product direction
Hestia is an **AI-assisted household environment management platform**, with a voice speaker as one of its interfaces—not a roleplay-centric voice chatbot. Three equal entry points (voice, responsive local Web UI, and authenticated API) share the same command, policy, and automation services. Primary non-functional goals: low resource use on N97-class Linux, flexible natural-language operation, and proactive but bounded optimization.

## Reuse-first architecture decision
Before implementing a component, evaluate existing OSS for features, resource use on N97, upkeep, API stability, and licenses. **Home Assistant is the first integration and reuse candidate** for device discovery, state, automations and integrations. Do not copy its entire feature set into Hestia or silently require a separate large stack: benchmark direct integration versus a self-contained lightweight mode, document trade-offs, and keep integrations replaceable. Evaluate MQTT and MCP as interoperable adapters. Use existing STT/TTS/wake-word components where feasible.

## Modules
1. **Host**: .NET worker/API, configuration, structured logging, lifecycle management (systemd).
2. **Input adapters**: CLI/text first; wake-word, VAD, STT and TTS later. Avoid always-streaming audio to external services.
3. **Provider adapters**: pluggable LLM interfaces, function/tool-call support or validated structured outputs. Timeout, rate limits and budgets.
4. **Command planner**: resolve intents into typed, inspectable action plans. Multi-step dependencies, conditions, cancellation and idempotency.
5. **Policy engine**: allowlisted actions, per-device scopes, explicit confirmation for consequential operations, dry-run and audit trails.
6. **Executor**: typed actions with bounded retries and rollback/compensation where possible; report partial failures truthfully.
7. **Automation**: persistent scheduler, event ingestion and rule engine; no mandatory LLM call per tick.
8. **Optimization**: suggest changes from measurements, preferences and goals; act only within a user-approved policy envelope.
9. **Integrations**: simulated devices first, then Home Assistant, MQTT, and MCP where useful.
10. **Web UI and API**: first-class responsive dashboard, device/status panels, AI cost, schedules, suggestions and administrative tools. Access control enforced server-side and shared with voice. Prefer a resource-efficient ASP.NET Core option chosen after benchmarking.
11. **Storage**: SQLite for policies, schedules and minimal local history, with retention and deletion controls.

## Google and notification ecosystem
- Official Google OAuth/API adapters are first-class integrations: Gmail, Calendar, Tasks and Drive. Docs/Sheets may follow after explicit demand.
- Use incremental least-privilege scopes, read-only defaults, secure per-user token storage, disconnect/revoke support and auditable opt-in writes.
- Expose calendar agenda, inbox summaries, task lists, integration health and unified notification center in Web UI; provide equivalent controlled voice commands.
- Do not indiscriminately sync or index mail and Drive content. Pass only required, authorized context to external AI providers.
- Preserve existing Alexa/SwitchBot usage during incremental migration; do not claim Alexa notification data is directly accessible. Reconstruct compatible delivery alerts from permitted sources such as email when available.
- Notification rules require opt-in, quiet hours, deduplication and privacy controls.
- See #17–#21.

## Trust boundaries
- Treat transcribed speech, model output, sensor payloads, remote tool descriptions and web content as untrusted input.
- Never grant shell execution, arbitrary network requests, file deletion or device access merely because a model requested it.
- Separate credentials from git; redact secrets and sensitive device identifiers from logs.
- Enforce authorization **after** LLM interpretation and **before** each side effect.
- Critical controls (locks, heating, security, power cutoff) must be disabled by default and require explicit opt-in with independent safeguards.
- Offline fallback: authorized pre-existing schedules and deterministic rules keep running; never silently fabricate current forecasts.

## First vertical slice
CLI input -> mock LLM -> JSON-schema validated action plan -> policy engine -> simulated light -> audit log.
Demonstrate compound commands, ambiguity clarification, deny-by-default, idempotency and offline behavior in tests.

## Open decisions
- Exact STT/TTS and wake-word stack after N97 benchmarking.
- Transport/API security for remote voice satellites.
- Third-party license review before fixing project license.
- Provider selection and API pricing based on current published offerings, not hard-coded model names.
