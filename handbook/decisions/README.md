# Decision records

Use an architecture decision record when a choice changes a durable cross-repository boundary, data contract, provider policy, privacy rule, ownership model, or operating procedure.

Repository-local implementation choices should stay with the owning repository.

## Naming

```text
YYYY-MM-DD-short-decision-title.md
```

## Template

```markdown
# Decision title

- Status: proposed | accepted | superseded
- Date: YYYY-MM-DD
- Owners:
- Related repositories and pull requests:

## Context

What changed or became necessary? Separate verified facts from assumptions.

## Decision

What boundary or behavior is being adopted?

## Consequences

What becomes easier, harder, required, or intentionally unsupported?

## Validation and rollout

What evidence, dependency order, canary, rollback, migration, or deployment is required?

## Supersedes / superseded by

Link any earlier or later decision.
```

Accepted records are historical evidence, not a substitute for validating current provider behavior, pricing, laws, deployment state, or live configuration.
