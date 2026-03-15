# Chore: Auto-Sync Shared Docs from Source Repos

## Chore ID

`CHORE-001`

## GitHub Issue

[#1](https://github.com/lwndev/ai-skills-docs/issues/1)

## Category

`configuration`

## Description

Set up automated daily syncing of documents from source documentation sites into this repo using `llms.txt` as the discovery mechanism. Both sources — agentskills.io and code.claude.com — publish `llms.txt` indexes, so the workflow auto-discovers pages without hardcoded file lists. Local filenames match source paths exactly for clean diffs and easy maintenance.

## Affected Files

- `sync-manifest.json` (new — defines llms-txt sources and destinations)
- `.github/workflows/sync-docs.yml` (new — daily cron workflow)
- `README.md` (updated to document sync process and naming convention)
- `docs/agent-skills/` (renamed files to match agentskills.io paths, added new files)
- `docs/anthropic/` (flattened from subdirectories to match code.claude.com's flat layout)

## Sources

| Source | Type | llms.txt URL | Destination |
|-|-|-|-|
| agentskills.io | `llms-txt` | `https://agentskills.io/llms.txt` | `docs/agent-skills/` |
| code.claude.com | `llms-txt` | `https://code.claude.com/docs/llms.txt` | `docs/anthropic/` |

## Acceptance Criteria

- [x] `sync-manifest.json` exists at the repo root with both sources configured as `llms-txt` type
- [x] Local filenames match source paths exactly (no renaming or prefixing)
  - `docs/agent-skills/` preserves source directory structure (`skill-creation/`, `client-implementation/`)
  - `docs/anthropic/` is flat, matching `code.claude.com/docs/en/` layout
- [x] GitHub Actions workflow `.github/workflows/sync-docs.yml` is created
  - Runs daily at 6:00 UTC (cron) and on manual trigger (`workflow_dispatch`)
  - Fetches each `llms.txt`, parses doc URLs, downloads files to mapped destinations
  - Opens a PR when changes are detected (does not auto-merge)
  - Removes stale `.md` files no longer present in the source index
  - Retains `git-repo` source type support for future use
- [x] All 64 Claude Code docs synced from code.claude.com
- [x] All 8 Agent Skills docs synced from agentskills.io (3 renamed, 5 new)
- [x] README documents the naming convention, sync process, and how to add new sources

## Completion

**Status:** `Completed`

**Completed:** 2026-03-15

**Pull Request:** [#2](https://github.com/lwndev/ai-skills-docs/pull/2)

## Notes

- Both sources use `llms-txt`, meaning new pages are picked up automatically — no manifest changes needed when a source adds or removes docs.
- The manifest JSON format is easily parsed by `jq` in the workflow.
- The workflow also supports `git-repo` sources (clone + rsync) for any future sources that don't publish an `llms.txt`.
- The `grep -oE` pattern (not `grep -oP`) is used for cross-platform compatibility (macOS + Linux).
