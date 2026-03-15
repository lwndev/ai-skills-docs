# Chore: Auto-Sync Shared Docs from Source Repos

## Chore ID

`CHORE-001`

## GitHub Issue

[#1](https://github.com/lwndev/ai-skills-docs/issues/1)

## Category

`configuration`

## Description

Set up automated daily syncing of documents from source repositories into this repo. For agentskills.io, use `llms.txt` as the index to discover available docs and their canonical paths. For all sources, local filenames must match the source filenames/paths so that diffs are clean and maintenance is straightforward. Includes creating a sync manifest, renaming existing files to match source names, and a GitHub Actions workflow on a daily cron schedule.

## Affected Files

- `sync-manifest.json` (new — defines source-to-destination mappings)
- `.github/workflows/sync-docs.yml` (new — daily cron workflow)
- `README.md` (update to document sync process and naming convention)
- `docs/agent-skills/` (rename files to match agentskills.io source paths)
- `docs/anthropic/` (rename files to match Anthropic source paths if applicable)

### File Renames (agent-skills)

Current local names do not match the agentskills.io source paths. Rename to match:

| Current Local Path | Source Path (agentskills.io) | New Local Path |
|-|-|-|
| `docs/agent-skills/agent-skills-oveview.md` | `home.md` | `docs/agent-skills/home.md` |
| `docs/agent-skills/agent-skills-specification.md` | `specification.md` | `docs/agent-skills/specification.md` |
| `docs/agent-skills/agent-skills-what-are-skills.md` | `what-are-skills.md` | `docs/agent-skills/what-are-skills.md` |

New files from agentskills.io not yet in this repo:

| Source Path | New Local Path |
|-|-|
| `client-implementation/adding-skills-support.md` | `docs/agent-skills/client-implementation/adding-skills-support.md` |
| `skill-creation/best-practices.md` | `docs/agent-skills/skill-creation/best-practices.md` |
| `skill-creation/evaluating-skills.md` | `docs/agent-skills/skill-creation/evaluating-skills.md` |
| `skill-creation/optimizing-descriptions.md` | `docs/agent-skills/skill-creation/optimizing-descriptions.md` |
| `skill-creation/using-scripts.md` | `docs/agent-skills/skill-creation/using-scripts.md` |

## Acceptance Criteria

- [ ] `sync-manifest.json` exists at the repo root and defines source-to-destination mappings
  - Each entry specifies: source type (`llms-txt` or `git-repo`), source URL/repo, source path, and destination path
  - For `llms-txt` sources, the workflow fetches the `llms.txt` index to discover files and their canonical paths
  - Covers `agent-skills/` (via agentskills.io/llms.txt) and `anthropic/` subdirectories
- [ ] Local filenames match source filenames/paths (no renaming or prefixing)
  - Existing misnamed files are renamed to match source paths (see rename table above)
  - Source directory structure (e.g., `skill-creation/`, `client-implementation/`) is preserved locally under `docs/agent-skills/`
- [ ] GitHub Actions workflow `.github/workflows/sync-docs.yml` is created
  - Runs on a daily schedule (cron)
  - Reads mappings from `sync-manifest.json`
  - For `llms-txt` sources: fetches `llms.txt`, parses doc URLs, downloads each file
  - For `git-repo` sources: clones/fetches repo and copies files to mapped destinations
  - Opens a PR when changes are detected (does not auto-merge)
  - Handles deleted or renamed source files (removes stale destinations)
- [ ] Workflow can also be triggered manually (`workflow_dispatch`)
- [ ] README documents the naming convention (match source names) and how to add new source mappings

## Completion

**Status:** `Completed`

**Completed:** 2026-03-15

**Pull Request:** [#2](https://github.com/lwndev/ai-skills-docs/pull/2)

## Notes

- The manifest should be the single source of truth for what gets synced and where, making it easy to add new source repos or paths without modifying the workflow itself.
- Consider JSON format for the manifest for easy parsing in the workflow.
- **Prefer `llms.txt` as the discovery mechanism** when a source provides one. The `llms.txt` file serves as a machine-readable index of available documentation, so the workflow can automatically discover new or removed pages without manifest updates. For sources without `llms.txt`, fall back to git repo cloning.
- The manifest should support two source types:
  - `llms-txt`: fetch the `llms.txt` URL, parse it for doc links, download each file. New pages are picked up automatically.
  - `git-repo`: clone a repo and copy specific paths. Requires explicit path mappings.
- **Naming convention**: local filenames must mirror source paths exactly. This makes diffs meaningful and avoids a layer of name translation that complicates maintenance.
- Anthropic docs may need to be fetched from public documentation URLs — check if Anthropic publishes an `llms.txt` and use it if available.
- Handle cases where source repos require authentication (use GitHub secrets/tokens).
