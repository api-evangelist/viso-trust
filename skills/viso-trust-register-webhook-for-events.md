---
name: Register a webhook for assessment and relationship events
description: Subscribe to VISO TRUST lifecycle events (assessment completed,
  recertification, relationship onboarded, artifact expiring, etc.) via an
  outbound webhook.
api: openapi/viso-trust-openapi-original.json
operations: [registerWebhook, getAllWebhooksForClient, getWebhookByIdForClient, updateWebhook, deleteWebhook]
---

# Register a webhook for events

Authenticate with `Authorization: Bearer <token>` against
`https://app.visotrust.com/api/v1`.

## Steps

1. **Register** — `POST /api/v1/webhooks` (`registerWebhook`) with:
   - `webhookUrl` — your HTTPS receiver.
   - `serviceType` — one of `GENERIC`, `SLACK`, `DISCORD`, `TEAMS`, `WORKATO`.
   - `eventTypes` — a set from: `ASSESSMENT_COMPLETED`,
     `ASSESSMENT_RECERTIFICATION_COMPLETED`, `ASSESSMENT_REMEDIATION_COMPLETED`,
     `ASSESSMENT_ARTIFACT_UPDATE_COMPLETED`, `DOCS_ONLY_ARTIFACT_UPDATE_COMPLETED`,
     `ASSESSMENT_REMINDER`, `ASSESSMENT_CANCELLED`, `ASSESSMENT_CANCELLED_BY_AUDITOR`,
     `ASSESSMENT_AUTOMATICALLY_CANCELLED`, `UPCOMING_RECERTIFICATION`,
     `RELATIONSHIP_ONBOARDED`, `RISK_ACCEPTED`, `RELATIONSHIP_OVERDUE`,
     `ARTIFACT_EXPIRING`, `ARTIFACT_EXPIRED`.
2. **List / inspect** — `GET /api/v1/webhooks` (`getAllWebhooksForClient`),
   `GET /api/v1/webhooks/{webhookId}` (`getWebhookByIdForClient`).
3. **Update** — `PUT /api/v1/webhooks` (`updateWebhook`) to change the URL or
   event set.
4. **Delete** — `DELETE /api/v1/webhooks/{webhookId}` (`deleteWebhook`).

## Rules
- `eventTypes` is a unique set; duplicates are collapsed.
- Prefer webhooks over polling `getAssessment` for completion.
