Agent Skills for use with [MailerLite](https://www.mailerlite.com/).

These skills follow the [Agent Skills specification](https://agentskills.io/specification) so they can be used by any skills-compatible agent, including Claude Code and Codex CLI.

## Installation

### Skills CLI (any agent)

Install with the [skills CLI](https://github.com/vercel-labs/skills) into Claude Code, Codex, Cursor, and 70+ other agents:

```
npx skills add mailerlite/mailerlite-skills
```

Or install a single skill for a specific agent:

```
npx skills add mailerlite/mailerlite-skills --skill email-marketing -a claude-code
```

### Claude Code Marketplace

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
| [email-marketing](skills/email-marketing) | Email marketing best practices for agents acting on a MailerLite account — safe sending rules, campaign and automation playbooks, segmentation, deliverability, and compliance |
