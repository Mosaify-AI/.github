# Product thesis

Mosaify is a general-purpose AI video generation platform.

It is not organized around briefs, campaigns, advertising workflows, or a single provider. The durable product is the connected creative loop: begin with an idea or reference, generate through the right model, direct the result, preserve context across iterations, and move toward a finished video.

## Product boundary

Mosaify should make these responsibilities feel like one system:

- generating video and supporting image assets;
- organizing projects, scenes, references, and outputs;
- choosing and routing to compatible models;
- preserving identity and creative context where the provider contract supports it;
- reviewing, iterating, downloading, and reusing results; and
- exposing the same product truth through web, API, CLI, and agent-facing tools.

Models, providers, and interfaces will change. The creative objects, user intent, safety boundaries, and ownership rules should remain coherent.

## Language standard

Prefer language such as **create**, **generate**, **direct**, **iterate**, **scene**, **reference**, **project**, **render**, and **video**.

Do not reintroduce campaign, brief, approval-pack, channel-export, ecommerce, or marketing-workflow framing unless Mosaify deliberately adopts a separate product with that scope.

## Decision test

When evaluating a feature, ask:

1. Does it help a creator generate or shape video?
2. Does it preserve a coherent workflow across models rather than expose provider complexity directly?
3. Is the consequential decision owned by the correct server, client, or provider boundary?
4. Can the result and its provenance be understood, reviewed, and reused?
5. Does the feature respect the privacy and consent contract documented in this handbook?
