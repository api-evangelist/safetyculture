---
name: safetyculture-subscribe-to-events
description: Register a webhook for SafetyCulture/Mitti trigger events, get the signing
  secret, and verify the subscription.
api: https://api.mitti.com
operations:
- WebhooksService_CreateWebhook
- WebhooksService_GetToken
- WebhooksService_ListWebhooks
- WebhooksService_GetWebhook
- WebhooksService_UpdateWebhook
- WebhooksService_DeleteWebhook
---

# Subscribe to Mitti events with webhooks

## Steps

1. **Create the webhook** (`WebhooksService_CreateWebhook`) with your HTTPS URL and the trigger events you want (e.g. `TRIGGER_EVENT_INCIDENT_CREATED`, `TRIGGER_EVENT_ACTION_STATUS_UPDATED`; the full list is in `asyncapi/safetyculture-webhooks.yml`).
2. **Fetch the signature secret** (`WebhooksService_GetToken`) and use it to verify incoming deliveries. Regenerating it (`WebhooksService_GenerateToken`) invalidates the old secret.
3. **Confirm** with `WebhooksService_ListWebhooks` / `WebhooksService_GetWebhook`.
4. **Maintain** with `WebhooksService_UpdateWebhook` to change events or URL, or `WebhooksService_DeleteWebhook` to unsubscribe.

## Conventions

- Base URL `https://api.mitti.com`; authenticate every call with `Authorization: Bearer {api_token}` (a user API token).
- Rate limits are per endpoint over a 60-second window; a throttled call returns `429 Too Many Requests`. Read the `x-ratelimit-*` headers and back off (see `rate-limits/`).
- No client-supplied idempotency key is documented (see `conventions/`), so do not blindly retry writes: after a timeout, re-read the resource with a list/get call before you resubmit.
- Prefer the current operations over the ones whose summary says `(legacy)`.
