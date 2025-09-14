# Security and privacy

Smart home documentation must clearly explain security trade-offs and privacy
controls.

## Secrets and credentials

Never store user tokens or keys in public repos. Use these patterns:

- Environment variables for local tools
- Encrypted secrets for CI
- Per-device long-lived tokens rotated quarterly

```text
# Good: DO NOT commit this
HOMESPHERE_API_KEY=sk_live_XXXXXXXX
```

## Privacy controls

1. Explain what data is collected (events, telemetry, audio snapshots).
2. Provide steps to opt out or purge data.
3. Offer export tools for users to download their activity history.

## Security checklist for releases

- [x] Threat model reviewed
- [x] Token rotation documented
- [ ] Third‑party audit scheduled

### Incident response

If a breach is suspected:

1. Revoke API keys and tokens.
2. Notify affected customers as required by law.
3. Publish a post‑mortem with timeline and remediation steps.
