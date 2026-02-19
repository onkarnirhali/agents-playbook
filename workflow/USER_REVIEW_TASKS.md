# User Review Tasks

This file is a human review backlog for items that should be revisited over time.

## How To Use

1. Pick any row with `status = pending` or `status = revisit`.
2. Review the linked files and current behavior.
3. Update `last_reviewed_on`, `next_review_on`, `status`, and `notes`.

## Review Task List

| review_id | area | task | linked_goals | status | priority | cadence | last_reviewed_on | next_review_on | notes |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| REV-PRIVACY-001 | Privacy + Data Controls | Review privacy/data controls end to end (API export/delete endpoints, UI accessibility, confirmation UX, deletion safety, retention alignment, and audit logging). | G-BETA-001, API-BETA-001, WEB-BETA-003 | pending | P0 | every 4 weeks | 2026-02-19 | 2026-03-19 | Focus files: `Auth-API/src/routes/meRoutes.js`, `Auth-API/src/controllers/privacyController.js`, `Auth-API/src/services/privacyService.js`, `client/src/components/privacy/PrivacyDialog.tsx`, `client/src/api/privacy.ts`, `Auth-API/README.md`. |
| REV-PRIVACY-002 | Privacy Policy Alignment | Validate that product wording and behavior match retention/export/delete controls and disclosures. | G-BETA-001 | pending | P1 | every 6 weeks | 2026-02-19 | 2026-04-02 | Confirm UI wording and docs remain aligned after each feature release. |
| REV-PRIVACY-003 | Security Hardening | Re-check sensitive data handling (no raw secrets/tokens in logs, events, or client storage). | G-BETA-001 | pending | P0 | every 4 weeks | 2026-02-19 | 2026-03-19 | Include API logs, event payloads, and extension/client storage paths. |

## Review Checklist For REV-PRIVACY-001

- [ ] Verify `/me/privacy/export` response contains only intended user-scoped fields.
- [ ] Verify `/me/privacy/delete` requires explicit confirmation and clears auth session cookies.
- [ ] Verify deletion impact on user-owned data is correct and no orphaned sensitive records remain.
- [ ] Verify UI export/download and delete flows are usable and clearly irreversible.
- [ ] Verify audit events exist for privacy export/delete requests and completion.
- [ ] Verify docs are up to date for privacy endpoints and expected behavior.
