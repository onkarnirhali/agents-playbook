# AGENTS Core

This repository contains shared governance standards for the Might As Well product repositories.

## Usage

Each product repository should include this repository as a submodule at `docs/agents/_core_src`.

Local docs in each product repository must include:
- `AGENTS.md`
- `docs/agents/REPO_SCOPE.md`
- `docs/agents/GOALS_REPO.md`
- `docs/agents/GOALS_AGENT.md`
- `docs/agents/CHANGE_LOG.md`
- `docs/agents/RELEASE_STAGES.md`
- `docs/agents/PR_CHECKLIST.md`
- `docs/agents/OVERRIDES.md`

## Mandatory Gate

1. Every meaningful change must map to a `goal_id`.
2. If alignment is partial or none, the implementer must ask the user before continuing.
3. Verification evidence is required before marking a change approved.
4. All markdown cross references must remain valid.

## Core References

- `goals/GOALS_GLOBAL.md`
- `workflow/GOAL_ALIGNMENT_GATE.md`
- `standards/CODING_STANDARDS.md`
- `standards/SECURITY_PRIVACY_STANDARDS.md`
- `templates/GOALS_REPO_TEMPLATE.md`
- `templates/CHANGE_LOG_TEMPLATE.md`
- `versions/VERSION.md`
