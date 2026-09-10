# kirby-agent-security

*This skill is part of the [Kirby Skills Collection](https://github.com/markkirby125/kirby-skills-collection).*

A rigorous Standard Operating Procedure (SOP) for auditing, scanning, and validating third-party AI agent skills, plugins, and Model Context Protocol (MCP) servers prior to installation.

As agentic workflows transition to autonomous execution environments, third-party extensions represent a primary attack surface. This skill equips AI coding assistants with a strict dual-layer defence architecture (automated static scanning via NVIDIA Skill Spectre + manual behavioural audits) to prevent prompt injection, credential exfiltration, and supply chain poisoning.

## 🪄 The Magic Prompt

Copy and paste this directly to your AI (Cursor, Windsurf, Claude Code, Antigravity):

```markdown
@agent Please install the kirby-agent-security skill into this workspace.
1. Read the `SKILL.md` file from this repository: https://github.com/markkirby125/kirby-agent-security
2. Identify the correct rules system for our current environment (e.g., `.cursor/rules/` for Cursor, `.windsurfrules` for Windsurf, `.clinerules` for Cline, or `~/.agents/skills/` for Antigravity).
3. Save the contents appropriately.
4. Confirm when the installation is complete.
```

## Manual Installation

- **Cursor**: Save the contents of `SKILL.md` to `.cursor/rules/kirby-agent-security.mdc`
- **Windsurf**: Save the contents of `SKILL.md` to `.windsurfrules`
- **Antigravity**: Clone this repository directly into `~/.agents/skills/kirby-agent-security`

## Tech Stack

- **Format**: Markdown / YAML
- **Compatibility**: Antigravity, Claude Code, Cursor, Windsurf, Cline

## External Resources & Authority Links

- [NVIDIA / Security Scanner Toolkit](https://github.com/nvidia/)
- [Model Context Protocol (MCP) Official Documentation](https://modelcontextprotocol.io/)
- [OWASP Top 10 for Large Language Model Applications](https://owasp.org/www-project-top-10-for-large-language-model-applications/)
- [Anthropic: Mitigating Prompt Injection](https://docs.anthropic.com/claude/docs/mitigating-prompt-injection)
