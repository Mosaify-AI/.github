# Content provenance

## Role and current state

Pexels is an active provenance source for checked-in Gallery and starter media. Mosaify does not have a runtime Pexels API integration or Pexels credential in the audited repositories. Some seed/reference assets are also recorded as original AI-authored material; that provenance category is not a separate production service integration.

`mosaify-api` owns the Gallery provenance schema/ledger and seed validation. `mosaify-web` owns the checked-in starter-media attribution record. Runtime delivery comes from Mosaify-controlled assets, not Pexels source URLs.

## Evidence and prohibited content

For every third-party asset, preserve the source page, creator attribution, license URL, original filename/identity where available, checksum, and the reviewed local derivative relationship. For original AI-authored assets, record the source class and review evidence needed by the ledger.

Do not add unlicensed content, private media, customer uploads repurposed as examples, unclear likeness rights, misleading trademarks, unverifiable source URLs, or media whose checked-in bytes do not match the recorded checksum. A reachable public page is not by itself proof of rights or product suitability.

## Promotion, replacement, and rollback

Before promotion, validate provenance schema, checksum, actual decoding, poster/preview behavior, content/model/quality review, and a seed dry run. Keep development fixtures distinct from approved production content.

If rights, attribution, integrity, or quality becomes uncertain, remove the asset from discovery, preserve the minimum restricted evidence needed for review, and replace it only after the full provenance checks pass. Do not expose private review evidence or customer material in the public ledger.

There are no Pexels configuration variables in the current repositories. License terms and source availability may change, so revalidate them when an asset is added or materially repurposed.
