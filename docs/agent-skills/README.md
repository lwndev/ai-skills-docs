# Open Source Agent Skills Specification

This directory contains documentation from the open source Agent Skills project at [agentskills.io](https://agentskills.io).

## About This Documentation

The Agent Skills specification defines a vendor-neutral format for creating modular, reusable AI agent capabilities. This specification is designed to work across multiple AI tools and platforms.

**Key characteristics:**

- Vendor-neutral, open source specification
- Defines the core format (frontmatter, structure, resources)
- Can be implemented by any AI tool or platform
- Maintained at [agentskills.io](https://agentskills.io)

## Contents

Files are named to match their source paths on agentskills.io for easier maintenance.

| File | Description | Source |
|------|-------------|--------|
| `home.md` | Overview of the Agent Skills concept | [agentskills.io/home](https://agentskills.io/home) |
| `what-are-skills.md` | Introduction to what skills are | [agentskills.io/what-are-skills](https://agentskills.io/what-are-skills) |
| `specification.md` | Complete format specification | [agentskills.io/specification](https://agentskills.io/specification) |
| `client-implementation/adding-skills-support.md` | Guide for adding skills support to an agent | [agentskills.io/client-implementation/adding-skills-support](https://agentskills.io/client-implementation/adding-skills-support) |
| `skill-creation/best-practices.md` | Best practices for skill creators | [agentskills.io/skill-creation/best-practices](https://agentskills.io/skill-creation/best-practices) |
| `skill-creation/evaluating-skills.md` | Evaluating skill output quality | [agentskills.io/skill-creation/evaluating-skills](https://agentskills.io/skill-creation/evaluating-skills) |
| `skill-creation/optimizing-descriptions.md` | Optimizing skill descriptions | [agentskills.io/skill-creation/optimizing-descriptions](https://agentskills.io/skill-creation/optimizing-descriptions) |
| `skill-creation/using-scripts.md` | Using scripts in skills | [agentskills.io/skill-creation/using-scripts](https://agentskills.io/skill-creation/using-scripts) |

## Document Index

The full list of available documents can be fetched from: https://agentskills.io/llms.txt

## Relationship to Anthropic's Documentation

Anthropic's Claude Code implements the Agent Skills format with some vendor-specific extensions and behaviors. While this specification defines the core format, Claude Code's documentation describes their specific implementation details.

See `docs/anthropic/skills/` for Anthropic's Claude Code-specific documentation.
