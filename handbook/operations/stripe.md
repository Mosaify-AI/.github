# Stripe

## Role and current state

Stripe supports checkout, subscriptions, top-up credits, Customer Portal sessions, signed webhooks, and authoritative billing reconciliation. The integration is merged and has sandbox evidence. Live-mode production enablement is not confirmed by public repository evidence.

`mosaify-api` owns plan truth, Stripe API calls, webhook verification, idempotent settlement, and the credit ledger. `mosaify-web` may request a checkout or portal session and navigate to the returned provider-hosted URL; it does not handle card data.

## Data boundary

Mosaify may process the minimum Stripe customer, subscription, product/price, checkout-session, invoice, event, and payment-status identifiers needed to reconcile entitlements and credits. Stripe-hosted surfaces process payment details. Never send card data, Stripe secret keys, webhook secrets, full webhook payloads, billing-session URLs, customer identifiers, or purchase contents into analytics, error monitoring, public docs, or client logs.

Configuration names are `STRIPE_SECRET_KEY`, `STRIPE_WEBHOOK_SECRET`, the ten `STRIPE_PRICE_*` variables listed in the catalog, and `CREDITS_ENFORCEMENT`.

## Rollout

1. Keep development/test and live products, prices, credentials, webhook endpoints, and portal settings separated.
2. Apply additive billing/ledger schema changes before application code.
3. Deploy API support with `CREDITS_ENFORCEMENT=off`, then deploy compatible web recovery paths.
4. Canary checkout, top-up, portal access, signed webhook handling, duplicate/out-of-order events, reconciliation, cancellation, and bucket preservation with controlled transactions.
5. Enable credit enforcement only after those paths succeed and rollback has been exercised.

## Rollback, retention, and alerting

Turn `CREDITS_ENFORCEMENT` off to stop enforcement without deleting the ledger. Disable checkout creation separately from webhook ingestion so already-issued events can still reconcile. Never roll back by deleting billing history or credit entries.

Retain first-party billing and ledger records for the legal, accounting, dispute, and entitlement purposes approved for the business; the exact production duration is unconfirmed and must be established with counsel. Alert on signature failures, sustained webhook errors, reconciliation drift, duplicate-credit protection failures, and checkout availability without placing customer or payment data in alerts.
