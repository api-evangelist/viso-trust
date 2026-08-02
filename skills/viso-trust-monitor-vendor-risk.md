---
name: Monitor vendor risk with external intelligence
description: Pull a vendor's risk summary and generate or retrieve external
  intelligence reports (SecurityScorecard, Recorded Future, BitSight).
api: openapi/viso-trust-openapi-original.json
operations: [getVendorRiskSummaryByNameOrDomain, createSecurityScorecardIntelligenceReport, createBitsightIntelligenceReport, getIntelligenceReportsByVendor, getLatestIntelligenceReport]
---

# Monitor vendor risk with external intelligence

Authenticate with `Authorization: Bearer <token>` against
`https://app.visotrust.com/api/v1`.

## Steps

1. **Get the risk summary** — `GET /api/v1/vendors/risk-summary`
   (`getVendorRiskSummaryByNameOrDomain`) by vendor name or domain, or
   `GET /api/v1/vendors/{id}/risk-summary` (`getVendorRiskSummaryById`).
2. **Generate an intelligence report** — POST to the source you use:
   `createSecurityScorecardIntelligenceReport`,
   `createBitsightIntelligenceReport`, or
   `createRecordedFutureIntelligenceReport`. Bulk variants exist
   (`.../bulk`) for many vendors at once.
3. **Retrieve reports** — `GET /api/v1/external-intelligence-reports/vendor/{vendorDomain}`
   (`getIntelligenceReportsByVendor`) for all reports, or
   `.../latest/{source}` (`getLatestIntelligenceReport`) for the newest from one
   source.

## Rules
- Reports are keyed by `vendorDomain`.
- Bulk endpoints accept arrays and return a per-item result envelope.
