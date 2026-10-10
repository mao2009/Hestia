# Security and Privacy Baseline

Hestia may control real physical devices. Safety and household privacy are design requirements, not optional polish.

- No telemetry code or background analytics.
- No API keys, household addresses, private IPs, access tokens, household speech recordings or real sensor traces in Git.
- Default local-only interfaces; remote access requires authentication and encrypted transport.
- Bind tools to explicit capabilities and scope permissions to the exact device and action.
- Treat every LLM-generated tool call as an untrusted proposal. Validate types, arguments and policy before execution.
- Confirm risky/destructive actions separately; high-risk devices must be opt-in and may remain unsupported.
- Rate-limit, budget, cancel and log automation with secret redaction.
- Minimize history; provide configurable retention, export and deletion.
- Provide a physical microphone-mute recommendation and clearly display active listening state.
- Do not allow arbitrary OS shell commands or generalized filesystem access in the first release.

**Security reporting:** Until a dedicated private reporting channel is configured, avoid sharing exploit details, keys, or home-network information in public issues.
