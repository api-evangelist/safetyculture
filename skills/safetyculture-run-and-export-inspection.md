---
name: safetyculture-run-and-export-inspection
description: Find a template, start an inspection, complete it, and export it to PDF
  or Word.
api: https://api.mitti.com
operations:
- ThePubService_SearchTemplates
- TemplatesService_GetTemplateByID
- InspectionService_CreateInspection
- InspectionService_CompleteInspection
- InspectionService_GetInspection
- ReportsService_StartInspectionExport
---

# Run and export an inspection

## Steps

1. **Find the template** with `ThePubService_SearchTemplates`, then read it with `TemplatesService_GetTemplateByID`.
2. **Create the inspection** from that template (`InspectionService_CreateInspection`). `ThePubService_StartInspection` is the older equivalent and can pre-fill answers.
3. **Complete it** (`InspectionService_CompleteInspection`), then read the result back with `InspectionService_GetInspection`.
4. **Export it** to PDF or Word with `ReportsService_StartInspectionExport`.
5. **For bulk sync**, use the data feeds (`ThePubService_FeedInspections`, `ThePubService_FeedInspectionItems`) rather than fetching inspections one at a time.

## Conventions

- Base URL `https://api.mitti.com`; authenticate every call with `Authorization: Bearer {api_token}` (a user API token).
- Rate limits are per endpoint over a 60-second window; a throttled call returns `429 Too Many Requests`. Read the `x-ratelimit-*` headers and back off (see `rate-limits/`).
- No client-supplied idempotency key is documented (see `conventions/`), so do not blindly retry writes: after a timeout, re-read the resource with a list/get call before you resubmit.
- Prefer the current operations over the ones whose summary says `(legacy)`.
