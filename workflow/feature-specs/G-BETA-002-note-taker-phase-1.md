---
goal_id: G-BETA-002
title: Note Taker Capability - Phase 1 (Notes Only, OCR Deferred)
stage: Beta
status: approved
owner: product
repos:
  - client
  - Auth-API
created_on: 2026-02-19
approved_on: 2026-02-19
approved_by: Product Stakeholder (Onkar)
---

# Note Taker Capability - Phase 1 (Notes Only, OCR Deferred)

## Summary

- Deliver Notes capability in Phase 1 without OCR extraction.
- Enforce password-protected note access at API level.
- Reuse Notes components in the Todo create/edit flow.
- Use this spec as baseline reference for G-BETA-002 behavior completeness.

## Scope

- In scope:
- Top navigation entry to Notes page and back navigation behavior.
- Notes list and grid views with persisted user preference.
- Create, view, edit, delete notes.
- Rich text note authoring with formatting controls.
- Password protection enable/disable and protected open flow.
- Note linking to Todo tasks with many-to-many mapping.
- Reusable note flows inside Todo modal (`New Note`, `Link Existing Notes`).
- Deferred note creation in Todo flow until Todo save succeeds.

- Out of scope:
- OCR ingestion, OCR extraction, OCR usage controls, and file upload processing.
- Note sharing/collaboration across users.

## User Flow (Click by Click)

- User clicks `Notes` button in top nav.
- System navigates to Notes page.
- User can return to dashboard/todos using nav/back action.
- User sees Notes page with `Add New Note` button and `List`/`Grid` controls on top-right.
- User toggles `List` or `Grid`.
- System updates view immediately and persists preference for that user.
- User clicks `Add New Note`.
- System opens note modal with title, rich-text editor, toolbar controls, save/cancel, and `Password Protect` checkbox.
- User uses formatting controls: bold, italic, underline, hyperlink, code snippet, quote, bullet list, numbered list.
- User checks `Password Protect`.
- System expands modal to show password and confirm-password fields.
- User enters both passwords.
- Save is enabled only when passwords match and minimum length is valid.
- User clicks save for standalone note.
- System creates note for user and shows note in list/grid.
- If protected, note shows lock icon and hides preview text.
- User opens an existing unprotected note.
- System navigates to note detail page in read-only mode.
- User can enable edit toggle beside text controls.
- User saves changes and formatting remains preserved on reopen.
- User opens a protected note.
- System blocks background and requests password before content is shown.
- User enters wrong password.
- System shows generic error and allows retry (rate-limited).
- User enters correct password.
- System opens note detail in read-only mode with edit toggle available.
- User enables password protection on existing note.
- System requires password and confirmation, then saves protected state.
- User disables password protection.
- System requires current note password.
- On success, password hash is removed and note becomes unprotected.
- User opens Todo create/edit modal and clicks `Add Notes`.
- System shows dropdown options `New Note` and `Link Existing Notes`.
- User clicks `New Note`.
- System opens reusable note modal and collects note draft details.
- Draft note stays local to Todo modal and is not persisted yet.
- User clicks `Link Existing Notes`.
- System opens modal listing existing user notes from Notes list API.
- User selects notes and clicks `Link`.
- System shows linked notes inline as removable chips in Todo modal.
- User clicks `Save` in Todo modal.
- System atomically creates/updates todo, creates deferred notes, and links notes to task.
- If Todo save fails, deferred notes and links are not persisted.

## Behavior Coverage

- Existing notes always open in read-only mode first.
- Edit toggle is shown only for existing notes and hidden during create flow.
- Protected notes always require password on each open.
- Protected note previews are hidden in list/grid.
- Notes belong to the authenticated user and enforce ownership checks.
- Duplicate note-to-task links are prevented.
- Deleting a note linked to tasks requires explicit confirmation.
- Confirmed delete removes note and all task links for that note.

## Edge Cases and Failure Paths

- Password mismatch keeps save disabled.
- Password below minimum length is rejected.
- Wrong password attempts return generic failure response.
- Unlock endpoint is rate-limited.
- Protected note content must never leak in list payloads.
- Canceling create note modal does not persist data.
- Canceling Todo modal discards deferred new notes.
- Todo save error keeps note-link transaction from partially persisting.
- Re-linking same note to same task is idempotent.
- Deleting todo removes links only, not standalone notes.

## Implementation Plan

- Frontend:
- Add Notes routes and page-level layout integration.
- Build reusable `NoteEditor` with TipTap and editor JSON state.
- Build `NoteEditorModal`, `NoteUnlockDialog`, and protection controls.
- Add Notes list/grid components with lock indicators and hidden previews.
- Add `Add Notes` dropdown and link/new-note flows in Todo modal.
- Persist notes view preference per user.

- Backend:
- Add notes routes, controller, service, and validation modules.
- Add note password hashing and verification utility.
- Add protected-note open endpoint with rate limiting.
- Extend todo create/update contracts with notes payload for deferred linking.
- Execute note creation and task-linking in transactional flow.
- Add events/audit entries for note lifecycle and protection actions.

- Data model:
- Add `notes` table.
- Add `note_task_links` table for many-to-many mapping.
- Add `users.notes_view_mode` for view preference persistence.

## Acceptance Checklist

- [ ] Governance gate: meaningful feature change without spec is blocked.
- [ ] Governance gate: spec with `status: draft` is blocked.
- [ ] Governance gate: spec with `status: approved` allows implementation.
- [ ] Notes page supports list/grid toggle and persists preference.
- [ ] Create note modal includes required rich-text controls.
- [ ] Password-protected notes enforce pre-open password check.
- [ ] Existing notes open read-only first with edit toggle support.
- [ ] Disable password protection requires current password and removes stored password hash.
- [ ] Todo `Add Notes` supports `New Note` and `Link Existing Notes`.
- [ ] Deferred new notes in Todo flow persist only when Todo save succeeds.
- [ ] Many-to-many note-task linking behavior is implemented and duplicate links are prevented.
- [ ] Linked note deletion prompt and unlink-on-confirm behavior is implemented.
- [ ] Validation, loading, empty, and error paths are documented in verification notes.

## Phase Split Reference

- Phase 1: Notes capability only (this spec).
- Phase 2: OCR extraction path and usage controls are deferred to mobile phase planning under `G-FINAL-001`.
