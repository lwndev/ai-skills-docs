# Anthropic Skills Documentation

This directory contains local copies of Anthropic's official documentation for Claude Code Agent Skills.

## About This Documentation

Anthropic maintains documentation for their implementation of Agent Skills within Claude Code. This documentation is specific to how Claude Code discovers, loads, and executes skills.

**Key characteristics:**

- Vendor-specific to Claude Code
- Covers Claude Code's skill loading behavior and frontmatter fields
- Includes best practices tailored to Claude's capabilities
- Maintained at [platform.claude.com](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview)

## Contents

| File | Description | Source |
|------|-------------|--------|
| `agent-skills-overview.md` | Overview of how Agent Skills work in Claude Code | [Link](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview) |
| `agent-skills-quickstart.md` | Quick start guide for creating skills | [Link](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/quickstart) |
| `agent-skills-best-practices.md` | Best practices for writing effective skills | [Link](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices) |
| `extend-claude-with-skills.md` | Guide to extending Claude Code with skills | [Link](https://code.claude.com/docs/en/skills) |
| `using-agent-skills-with-the-api.md` | Using Agent Skills with the Claude API | [Link](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview) |

## Relationship to Open Source Specification

The open source Agent Skills specification at [agentskills.io](https://agentskills.io) defines a vendor-neutral format that multiple AI tools can support. Anthropic's documentation describes how Claude Code specifically implements and extends this format.

See `docs/agent-skills/` for the open source specification.
