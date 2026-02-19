---
goal_id: G-XXXX-000
title: Feature Title
stage: Alpha
status: draft
owner: team-or-role
repos:
  - client
  - Auth-API
created_on: YYYY-MM-DD
approved_on: null
approved_by: null
---

# {{ title }}

## Summary

- State the feature objective and non-objective in concise bullets.

## Scope

- In scope:
- Out of scope:

## User Flow (Click by Click)

- Step-by-step user journey from entrypoint to completion.
- Include alternate and return paths.

## Behavior Coverage

- Define expected behavior for each user action.
- Define read-only, edit, navigation, and state persistence behavior where applicable.

## Edge Cases and Failure Paths

- Validation errors and mismatches.
- Permission/ownership enforcement.
- Empty/loading/error states.
- Retry and rate-limit behavior where relevant.
- Cancellation, rollback, and idempotency behavior.

## Implementation Plan

- Frontend implementation plan.
- Backend implementation plan.
- Data model and migration plan.
- Reusability and modularity plan.

## Acceptance Checklist

- [ ] User flow is fully implemented end-to-end.
- [ ] Expected behaviors match this spec.
- [ ] Edge cases and failure paths are covered.
- [ ] API/data contract changes are implemented and documented.
- [ ] Verification evidence is captured (tests, build, or manual validation).
- [ ] Traceability from implementation to this spec is documented.
