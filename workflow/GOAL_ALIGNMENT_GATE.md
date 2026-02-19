# Goal Alignment Gate

## Purpose

Ensure every code or configuration change stays aligned to approved product goals.

## Required Rule Set

1. Assign exactly one primary `goal_id` per change set.
2. Secondary goals may be listed, but only one primary goal can drive acceptance.
3. Alignment must be one of:
- `direct`
- `partial`
- `none`
4. If alignment is `partial` or `none`, the implementer must ask user clarification before merging.
5. A change cannot be marked `approved` without verification evidence.
6. Every meaningful feature change must have exactly one feature spec file under `workflow/feature-specs/`.
7. Feature implementation must follow this sequence: `Spec Draft -> Flow/Behavior Review -> Spec Approved -> Implementation`.
8. Feature spec frontmatter is required and must include:
- `goal_id`
- `title`
- `stage`
- `status` (`draft` or `approved`)
- `owner`
- `repos`
- `created_on`
- `approved_on`
- `approved_by`
9. Hard block rule: if a meaningful feature spec is missing or `status != approved`, implementation must not begin.
10. If blocked by missing or unapproved spec, request user flow and behavior clarification before implementation.

## Meaningful Feature Change

Treat a change as meaningful when it adds or modifies user-visible behavior, API behavior, data contracts, workflows, or product logic.

Do not treat docs-only edits or trivial non-behavioral changes as meaningful feature implementation.

## Feature Spec Content Contract

Each feature spec must include:

- Click-by-click user flow
- Expected user behavior coverage
- Edge cases and failure paths
- Implementation plan
- Acceptance checklist used for validation traceability

## Verification Evidence

At least one of the following is required:

- Test output summary
- Build output summary
- Manual validation notes with exact steps
- API contract check proof

## Block Conditions

Block and request user input when:

- No goal mapping exists
- Goal mapping is invalid
- Change expands scope beyond stated goal
- Required documentation updates are missing
- Meaningful feature spec file is missing
- Feature spec exists but frontmatter `status` is `draft` or missing

## Change Log Contract

Each accepted change entry must include:

- `change_id`
- `date`
- `goal_id`
- `alignment`
- `summary`
- `verification`
- `decision`
