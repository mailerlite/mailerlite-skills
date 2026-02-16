Agent Skills for use with [MailerLite](https://www.mailerlite.com/).

These skills follow the [Agent Skills specification](https://agentskills.io/specification) so they can be used by any skills-compatible agent, including Claude Code and Codex CLI.

## Installation

### Marketplace

```
/plugin marketplace add mailerlite/mailerlite-skills
/plugin install mailerlite@mailerlite-skills
```

### Manually

#### Claude Code

Add the contents of this repo to a `/.claude` folder in the root of your project. See more in the [official Claude Skills documentation](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview).

#### Codex CLI

Copy the `skills/` directory into your Codex skills path (typically `~/.codex/skills`). See the [Agent Skills specification](https://agentskills.io/specification) for the standard skill format.

## Skills

| Skill | Description |
|-------|-------------|
| [mailerlite-cli](skills/mailerlite-cli) | Manage subscribers, campaigns, automations, groups, forms, e-commerce, and more using the [MailerLite CLI](https://github.com/mailerlite/mailerlite-cli) |
