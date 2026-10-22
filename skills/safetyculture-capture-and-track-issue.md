---
name: safetyculture-capture-and-track-issue
description: Submit an issue, assign collaborators, move its status, comment on it,
  and list issues.
api: https://api.mitti.com
operations:
- CustomerConfigurationService_GetCategories
- IncidentsService_SubmitIncident
- IncidentsService_AddCollaborators
- IncidentsService_UpdateStatus
- TimelineService_AddComment
- IncidentsService_GetIncidents
- IncidentsService_GetIncidentById
---

# Capture and track an issue

## Steps

1. **Pick a category** with `CustomerConfigurationService_GetCategories`.
2. **Submit the issue** (`IncidentsService_SubmitIncident`). Use this rather than `IncidentsService_CreateIncident`, which is marked legacy.
3. **Assign people** (`IncidentsService_AddCollaborators`).
4. **Move it through its workflow** (`IncidentsService_UpdateStatus`) and record notes with `TimelineService_AddComment`.
5. **Reconcile** with `IncidentsService_GetIncidents` (a POST list with filters) or `IncidentsService_GetIncidentById`. To avoid polling, subscribe to `TRIGGER_EVENT_INCIDENT_*` webhooks (see the events skill).

## Conventions

- Base URL `https://api.mitti.com`; authenticate every call with `Authorization: Bearer {api_token}` (a user API token).
- Rate limits are per endpoint over a 60-second window; a throttled call returns `429 Too Many Requests`. Read the `x-ratelimit-*` headers and back off (see `rate-limits/`).
- No client-supplied idempotency key is documented (see `conventions/`), so do not blindly retry writes: after a timeout, re-read the resource with a list/get call before you resubmit.
- Prefer the current operations over the ones whose summary says `(legacy)`.
