# Bug: Workflow YAML Syntax Error

## Bug ID

`BUG-001`

## GitHub Issue

[#4](https://github.com/lwndev/ai-skills-docs/issues/4)

## Category

`runtime-error`

## Severity

`high`

## Description

The GitHub Actions workflow `.github/workflows/sync-docs.yml` fails YAML validation with "You have an error in your yaml syntax on line 159", preventing the sync workflow from running entirely.

## Steps to Reproduce

1. Push any change to `main` or trigger the `sync-docs` workflow via `workflow_dispatch`
2. GitHub Actions rejects the workflow file before execution

## Expected Behavior

The workflow file passes YAML validation and the sync job runs successfully.

## Actual Behavior

GitHub reports: `Invalid workflow file: .github/workflows/sync-docs.yml#L159 — You have an error in your yaml syntax on line 159`. The workflow never executes.

## Root Cause(s)

1. In `.github/workflows/sync-docs.yml:155-167`, the `gh pr create` command uses a `$(cat <<EOF ... EOF)` heredoc to build the PR body. The heredoc content (lines 158-165) is not indented under the YAML `run: |` block — it starts at column 0. YAML's block scalar parser requires all content lines to be indented at least as much as the first content line of the block. The unindented `EOF` delimiter and heredoc body cause the YAML parser to interpret them as top-level YAML keys rather than continuation of the `run` script, breaking the parse at line 159.

## Affected Files

- `.github/workflows/sync-docs.yml`

## Acceptance Criteria

- [ ] The heredoc body and `EOF` delimiter are indented to match the surrounding YAML block scalar indentation (RC-1)
- [ ] The workflow file passes YAML validation (`yamllint` or GitHub Actions syntax check) (RC-1)
- [ ] The `gh pr create` command still produces a correctly formatted PR body with expanded `sources_list` variable (RC-1)

## Completion

**Status:** `Completed`

**Completed:** 2026-03-15

**Pull Request:** [#5](https://github.com/lwndev/ai-skills-docs/pull/5)

## Notes

- Introduced in PR #3 (`fix/sync-workflow-issues`) when the heredoc was changed from a single-quoted `<<'EOF'` (which had a variable expansion bug) to an unquoted `<<EOF`
- The fix must keep the unquoted `EOF` so that `${sources_list}` expands, while indenting the heredoc body to satisfy the YAML parser
