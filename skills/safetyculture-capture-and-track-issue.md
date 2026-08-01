---
name: Capture and track an issue
description: Submit an issue, assign collaborators, update its status, and list issues in SafetyCulture.
api: https://api.safetyculture.io
operations:
  - incidentsservice_submitincident
  - incidentsservice_addcollaborators
  - incidentsservice_updatestatus
  - incidentsservice_getincidents
---

# Capture and track an issue

Authenticate with `Authorization: Bearer {api_token}` against
`https://api.safetyculture.io`.

## Steps

1. **Submit the issue** (`incidentsservice_submitincident`) with a title, description,
   category, site, and (optionally) an occurred-at timestamp in RFC 3339.
2. **Assign collaborators** (`incidentsservice_addcollaborators`) so the right people
   own and act on it.
3. **Update status** (`incidentsservice_updatestatus`) as the issue moves through its
   workflow (e.g. open -> in progress -> resolved).
4. **List / reconcile** (`incidentsservice_getincidents`) with filters and pagination
   to poll open issues, or subscribe to `TRIGGER_EVENT_INCIDENT_*` webhooks instead of
   polling (see the events skill).

## Conventions

- Use the newer submit/get issue operations rather than the `legacy` variants
  (`incidentsservice_createincident` / `incidentsservice_getincident`) — see
  `lifecycle/safetyculture-lifecycle.yml`.
- Respect 429 rate limits and `x-ratelimit-*` headers (`rate-limits/`).
