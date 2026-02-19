# Feature Specs Workflow

This folder is the canonical location for approved feature specifications.

## Hard Block Rule

- No meaningful feature implementation may begin until an approved spec exists in this folder.
- Approval source of truth is spec frontmatter `status: approved`.
- If spec is missing or `status` is not approved, the change is blocked.

## Scope of Rule

- Applies to all meaningful feature changes.
- Does not apply to docs-only changes or trivial non-behavioral edits.

## Required Workflow

1. Draft spec file from `SPEC_TEMPLATE.md`.
2. Review click-by-click user flow and behavior with stakeholders.
3. Capture edge cases and implementation plan.
4. Mark spec frontmatter as approved.
5. Start implementation.

## Required Frontmatter Contract

Every spec must define:

- `goal_id: string`
- `title: string`
- `stage: Alpha|Beta|Final`
- `status: draft|approved`
- `owner: string`
- `repos: string[]`
- `created_on: YYYY-MM-DD`
- `approved_on: YYYY-MM-DD|null`
- `approved_by: string|null`

## Required Spec Body Contract

Every spec must include:

- Click-by-click user flow
- Expected behavior coverage
- Edge cases and failure paths
- Implementation plan
- Acceptance checklist

## Naming Convention

- Use goal-prefixed filenames.
- Example: `G-BETA-002-note-taker-phase-1.md`
