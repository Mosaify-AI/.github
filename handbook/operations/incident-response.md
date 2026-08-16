# Incident response

Use this process for security, privacy, availability, billing, provider, and data-integrity incidents.

## Severity

| Level | Meaning | Examples |
| --- | --- | --- |
| SEV-1 | Active widespread harm or critical compromise | Credential exposure, cross-workspace data access, destructive billing or data corruption |
| SEV-2 | Material production impact with a contained boundary | Generation unavailable, telemetry collecting prohibited data, purchases failing broadly |
| SEV-3 | Localized or degraded behavior with a safe workaround | One provider or model failing, noisy alerts, delayed non-critical processing |

When uncertain between two severities, start at the higher level and downgrade after evidence narrows the impact.

## Response loop

1. **Declare.** Name an incident lead, severity, start time, affected environments, and the currently known user impact.
2. **Contain.** Disable the narrowest affected capture, provider, route, worker, or deployment path. Preserve unrelated service availability.
3. **Protect evidence.** Record timestamps, release identifiers, request IDs, and sanitized failure signatures. Do not copy secrets, private payloads, or customer media.
4. **Diagnose.** Separate confirmed observations from hypotheses. Identify the owning repository and external system.
5. **Recover.** Prefer a known rollback or configuration disable. Validate with a narrow canary before restoring normal traffic.
6. **Communicate.** Keep a short timeline and state what is confirmed, mitigated, still unknown, and next.
7. **Learn.** Produce a blameless follow-up with root cause, contributing conditions, detection gap, corrective owners, and deadlines.

If an incident includes private data, keep detailed evidence in the approved restricted system and link to it by access-controlled reference.
