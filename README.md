# AI Skills Docs

Shared reference documentation for Claude Code skills, hooks, agents, plugins, and the [agent-skills.io](https://agentskills.io) specification.

This repository is designed to be included as a git submodule in projects that need access to these reference materials.

## Structure

```
docs/
├── agent-skills/            # agentskills.io open specification
│   ├── agent-skills-specification.md
│   ├── agent-skills-oveview.md
│   └── agent-skills-what-are-skills.md
└── anthropic/               # Anthropic's official documentation
    ├── agents/
    │   └── sub-agents.md
    ├── hooks/
    │   ├── hooks-guide.md
    │   └── hooks-reference.md
    ├── plugins/
    │   ├── create-plugins.md
    │   └── plugins-reference.md
    └── skills/
        ├── agent-skills-best-practices.md
        ├── agent-skills-overview.md
        ├── agent-skills-quickstart.md
        ├── extend-claude-with-skills.md
        └── using-agent-skills-with-the-api.md
```

## Usage as a submodule

```bash
# Add to your project
git submodule add https://github.com/lwndev/ai-skills-docs.git docs/shared

# Update to latest
git submodule update --remote docs/shared
```
