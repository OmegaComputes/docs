---
name: pewter-payments-keys
description: Use when connecting an SI assistant to Pewter, managing API credentials, or explaining metered compute and payment availability.
---
# Pewter payments and API keys

## Current behavior (verified)

Reviewed against developer sources on 7 November 2026. Availability depends on the approved deployment. Use `https://api.example` only as a placeholder; obtain the approved API host separately.

- Developer documentation is a static site. It explains access but does not issue credentials or process payments.
- A signed-in human owner requests an `omk_` agent key with `POST /api/v1/agents/{id}/keys`, selecting scopes. The secret is returned at creation; store it securely and never paste it into a conversation or skill file.
- `pws_` is a human session from Apple/Google sign-in. `pck_` is a CLI credential issued through device-code login approved by a human. Device-code login does not issue a human session. CLI credentials cannot mint agent keys.
- Machine measurements arrive through signed heartbeats. Device/session observations and job running/GPU-seconds contribute to metering; delivery records roll into hourly tranches. Test-network ledger values are simulated, not cash.
- Real-money metered access is not available in the audited build. Card checkout is test-mode only; internal delivery funding is sandbox-only. See the Paying and payouts documentation for availability and draft pricing.
- Claude-compatible MCP OAuth support exists in the code. Use only the approved Pewter staging connector when configured; its running connection was not verified by this source review. Connector sign-in is not a payment receipt.

## Coming soon: required payment activation

These are target requirements, not a claim that the current server implements paid activation:

- No metered key activation without a successful charge or funded credit hold.
- Server-confirmed funding and atomic job/cycle reservations before paid work starts.
- Account/per-key spend caps and idempotent usage settlement.
- Suspension of metered access on failed payment or zero available balance, with bounded stopping of active work and reconciliation before reactivation.

A skill is guidance, not server-side enforcement. Do not promise paid access before the service announces availability and the server confirms it.

## Operating safely

1. Confirm the approved environment, account and supported connection method.
2. Use least-privilege credentials and the platform's secure credential storage.
3. Keep test funds separate from real payments; never treat a browser success screen as proof of a charge.
4. Obtain explicit approval before any purchase, funding, key creation or configuration change. Loading this skill authorizes none of those actions.
5. Report current capabilities separately from coming-soon requirements. Do not invent endpoints, payment receipts or runtime status.
