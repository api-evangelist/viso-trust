---
name: Onboard a vendor and run a risk assessment
description: Create a third-party relationship in VISO TRUST, onboard it, start a
  risk assessment, and retrieve the assessment summary.
api: openapi/viso-trust-openapi-original.json
operations: [createRelationshipAsCurrentUserByDomain, onboardRelationship, createAssessment, getAssessment, getAssessmentSummary, exportSummaryPdf]
---

# Onboard a vendor and run a risk assessment

Use the VISO TRUST Client API (`https://app.visotrust.com/api/v1`). Authenticate
every request with `Authorization: Bearer <token>` — the token is generated once
from the Dashboard user profile by an Admin or Program Manager.

## Steps

1. **Create the relationship** — `POST /api/v1/relationships/domain`
   (`createRelationshipAsCurrentUserByDomain`) with the vendor domain, or
   `POST /api/v1/relationships` (`createRelationshipAsCurrentUser`) for a full
   payload. Capture the returned relationship `id`.
2. **Onboard it** — `PUT /api/v1/relationships/{id}/onboard`
   (`onboardRelationship`) to move the relationship into the active lifecycle.
3. **Start the assessment** — `POST /api/v1/assessments` (`createAssessment`)
   referencing the relationship. Capture the assessment `id`.
4. **Poll for completion** — `GET /api/v1/assessments/{id}` (`getAssessment`).
   Prefer subscribing a webhook to `ASSESSMENT_COMPLETED` (see the webhook skill)
   over tight polling.
5. **Read the summary** — `GET /api/v1/assessments/{id}/summary`
   (`getAssessmentSummary`); export a PDF with
   `GET /api/v1/assessments/{id}/summary/export` (`exportSummaryPdf`).

## Rules
- Pagination on list endpoints uses `page` / `size` / `sort`.
- Only Admin or Program Manager tokens may call `/api/v1/*`.
- No idempotency key is supported; do not blindly retry POSTs — check for an
  existing relationship/assessment first.
