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

## Change Log Contract

Each accepted change entry must include:

- `change_id`
- `date`
- `goal_id`
- `alignment`
- `summary`
- `verification`
- `decision`
