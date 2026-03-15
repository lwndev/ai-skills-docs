# AI Skills Docs

Shared reference documentation for Claude Code skills, hooks, agents, plugins, and the [agent-skills.io](https://agentskills.io) specification.

This repository is designed to be included as a git submodule in projects that need access to these reference materials.

## Structure

```
docs/
├── agent-skills/                          # agentskills.io open specification
│   ├── home.md                            # Overview
│   ├── specification.md                   # Complete format specification
│   ├── what-are-skills.md                 # Introduction to skills
│   ├── client-implementation/
│   │   └── adding-skills-support.md       # Guide for adding skills support
│   └── skill-creation/
│       ├── best-practices.md              # Best practices for skill creators
│       ├── evaluating-skills.md           # Evaluating skill output quality
│       ├── optimizing-descriptions.md     # Optimizing skill descriptions
│       └── using-scripts.md              # Using scripts in skills
└── anthropic/                             # Claude Code docs from code.claude.com
    ├── skills.md                          # Extend Claude with skills
    ├── hooks.md                           # Hooks reference
    ├── hooks-guide.md                     # Hooks guide
    ├── sub-agents.md                      # Custom subagents
    ├── plugins.md                         # Create plugins
    ├── plugins-reference.md               # Plugins reference
    ├── best-practices.md                  # Best practices
    ├── overview.md                        # Claude Code overview
    ├── mcp.md                             # MCP integration
    ├── memory.md                          # Memory/CLAUDE.md
    ├── ...                                # All other code.claude.com docs
    └── The-Complete-Guide-to-Building-Skill-for-Claude.pdf
```

## Automated sync

Documentation is synced daily from source repositories via GitHub Actions. The sync process is defined by two files:

- **`sync-manifest.json`** — Defines source-to-destination mappings. Two source types are supported:
  - `llms-txt`: Fetches the `llms.txt` index from a documentation site to discover available pages and downloads each one. New pages are picked up automatically.
  - `git-repo`: Clones a repository and copies specific paths.
- **`.github/workflows/sync-docs.yml`** — Runs daily (and on manual trigger), reads the manifest, syncs files, and opens a PR when changes are detected.

### Naming convention

Local filenames match source filenames/paths exactly. This ensures diffs are clean and avoids a layer of name translation during maintenance. For example, `agentskills.io/specification.md` is stored as `docs/agent-skills/specification.md`.

### Adding a new source

To add a new source, add an entry to `sync-manifest.json`:

```json
{
  "name": "my-source",
  "type": "llms-txt",
  "llms_txt_url": "https://example.com/llms.txt",
  "destination": "docs/my-source",
  "description": "Description of what this source provides"
}
```

Or for a git repo:

```json
{
  "name": "my-repo",
  "type": "git-repo",
  "repo": "https://github.com/org/repo.git",
  "branch": "main",
  "mappings": [
    { "source": "docs/", "destination": "docs/my-repo/" }
  ],
  "description": "Description of what this source provides"
}
```

## Usage as a submodule

```bash
# Add to your project
git submodule add https://github.com/lwndev/ai-skills-docs.git docs/shared

# Update to latest
git submodule update --remote docs/shared
```
