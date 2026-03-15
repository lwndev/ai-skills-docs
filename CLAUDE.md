# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

A centralized documentation hub that auto-syncs reference docs from two sources into `docs/`. Designed to be included as a git submodule in projects that need Claude Code and Agent Skills documentation as context.

- `docs/agent-skills/` — Open Agent Skills specification from agentskills.io
- `docs/anthropic/` — Claude Code documentation from code.claude.com

## How the sync works

`sync-manifest.json` defines source-to-destination mappings. Both sources use the `llms-txt` type: the workflow fetches each source's `llms.txt` index, discovers all linked `.md` files, and downloads them. Stale files not in the index are removed (except `README.md` files).

The GitHub Actions workflow (`.github/workflows/sync-docs.yml`) runs daily at 6:00 UTC and on manual dispatch. When changes are detected, it opens a PR — it does not auto-merge.

## Naming convention

Local filenames match source paths exactly. For example, `agentskills.io/specification.md` becomes `docs/agent-skills/specification.md`. Do not rename synced files.

## Adding a new documentation source

1. Add an entry to `sync-manifest.json` with `name`, `type` (`llms-txt` or `git-repo`), URL/repo, `destination`, and `description`
2. The next workflow run will pick up the new source automatically

## Requirements documents

Task documentation lives in `requirements/` with subdirectories by type (`chores/`, `bugs/`, `features/`). Documents follow an ID convention (e.g., `CHORE-001-description.md`). Use the skill-based workflows (`/documenting-chores`, `/executing-chores`, etc.) to create and execute these.

## Commit message convention

This repo uses conventional commits with scope: `type(scope): description`. Examples from history:
- `chore(configuration): add auto-sync workflow`
- `fix(workflow): address sync-docs reliability issues`
- `chore(documentation): update requirements to match implementation`
