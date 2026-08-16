# System map

Mosaify is coordinated from `mosaify-workspace`, but each product repository has its own history and release lifecycle.

```mermaid
flowchart TB
    Workspace["mosaify-workspace<br/>coordination"]
    Web["mosaify-web<br/>browser product"]
    API["mosaify-api<br/>server authority"]
    CLI["mosaify-cli<br/>local generation client"]
    MCP["mosaify-mcp<br/>agent-facing tools"]
    Ava["Ava<br/>archived reference"]
    DB[("PostgreSQL")]
    Media["Durable media storage"]
    Provider["OpenAI / fal / BytePlus"]
    Billing["Stripe"]
    Identity["Google / Apple / SMTP"]
    Analytics["Consented analytics"]
    Errors["Error monitoring"]

    Workspace -. "coordinates" .-> Web
    Workspace -. "coordinates" .-> API
    Workspace -. "coordinates" .-> CLI
    Workspace -. "coordinates" .-> MCP
    Workspace -. "retains" .-> Ava
    Web --> API
    API --> DB
    API --> Media
    API --> Provider
    CLI --> Provider
    API --> Billing
    API --> Identity
    Web -. "after consent" .-> Analytics
    API -. "after valid consent" .-> Analytics
    Web -. "minimized errors" .-> Errors
    API -. "minimized errors" .-> Errors
```

## Repository ownership

| Repository | Owns | Does not silently own |
| --- | --- | --- |
| `mosaify-workspace` | Cross-repository conventions, bootstrap, local orchestration, and shared agent workflows | Product implementation or child-repository releases |
| `mosaify-web` | Browser presentation, user interaction, consent UI, and client-side telemetry gating | Billing truth, provider credentials, or authoritative render outcomes |
| `mosaify-api` | Authentication, authorization, persistence, generation orchestration, billing truth, and authoritative lifecycle events | Browser interaction or client-only presentation state |
| `mosaify-cli` | Local client workflows | Web product state or API database ownership |
| `mosaify-mcp` | Provider-agnostic agent tools and contracts | Private server state unless explicitly integrated |
| `Ava` | Archived reference implementation for agent-run contracts | Active product delivery or provider execution |

`mosaify-mcp` is currently a runnable stdio capability-discovery scaffold. Its API adapter is planned, not active. No production hosting vendor is established by the checked-in repositories.

## Cross-repository change rule

When a public contract changes, coordinate the producer and every consumer as separate pull requests. State deployment order and compatibility requirements explicitly. A passing check in one repository does not validate its siblings.
