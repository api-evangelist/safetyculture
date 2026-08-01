---
name: Subscribe to SafetyCulture events with webhooks
description: Register a webhook endpoint, subscribe to trigger event types, and verify delivery signatures for near real-time SafetyCulture events.
api: https://api.safetyculture.io
operations:
  - webhooksservice_createwebhook
  - webhooksservice_gettoken
  - webhooksservice_listwebhooks
---

# Subscribe to SafetyCulture events with webhooks

Authenticate every request with a bearer API token:
`Authorization: Bearer {api_token}` (see `authentication/safetyculture-authentication.yml`).
Base URL is `https://api.safetyculture.io`.

## Steps

1. **Create a webhook** (`webhooksservice_createwebhook`). Register the receiving URL in
   your application and subscribe to the `event_types` you care about — e.g.
   `TRIGGER_EVENT_INSPECTION_COMPLETED_STATUS`, `TRIGGER_EVENT_ACTION_CREATED`,
   `TRIGGER_EVENT_INCIDENT_CREATED`. The full event catalog is in
   `asyncapi/safetyculture-webhooks.yml`.
2. **Fetch the signature secret** (`webhooksservice_gettoken`). Use it to verify the
   authenticity of each incoming delivery before processing.
3. **List webhooks** (`webhooksservice_listwebhooks`) to confirm your subscription and
   audit existing endpoints.

## Payload

Each delivery carries `webhook_id`, `version`, an `event` object
(`date_triggered`, `event_types`, `triggered_by`), a `resource` (`id`, `type`), and a
`data` subset. Treat `data` as a pointer — fetch the full resource via its service API
when you need complete state.

## Conventions

- Respect rate limits (429 + `x-ratelimit-*` headers, see `rate-limits/`).
- Date/time values are RFC 3339 (`conventions/safetyculture-conventions.yml`).
