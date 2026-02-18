# Claude Code Plugin Marketplace

Reusable [Claude Code](https://claude.ai/code) plugins for Cloudflare Workers SaaS development and universal dev workflows.

## Plugins

### `cf-saas-stack`

Conventions and commands for building SaaS applications with **Cloudflare Workers + React Router v7 + tRPC + D1/Drizzle + Better Auth**.

- **15 rules** — Auth, database, error handling, i18n, Stripe, feature flags, and more
- **7 commands** — DB migrations, feature implementation, PostHog setup, feature flags
- **1 agent** — Data analytics dashboard generator

### `dev-workflows`

Universal dev workflows that work with any project.

- **9 rules** — Frontend tasks, Playwright tests, PR conventions, Tailwind, docs
- **11 commands** — Architecture tracking, PR creation/review, UX research, design research
- **6 agents** — Architecture tracker, context keeper, Figma validator, Figma-to-Tailwind converter, logger, tester

## Installation

### Add the marketplace

```bash
/plugin marketplace add SeanningTatum/claude-plugins
```

### Install a plugin

```bash
# Cloudflare SaaS stack conventions
/plugin install cf-saas-stack

# Universal dev workflows
/plugin install dev-workflows

# Install both
/plugin install cf-saas-stack dev-workflows
```

## What's Included

### Rules

Rules are automatically loaded into Claude Code's context and guide how it writes code. They cover conventions for authentication, database patterns, error handling, i18n, Stripe integration, testing, and more.

### Commands

Commands are slash-command workflows you can invoke (e.g., `/db-migration`, `/implement-feature`, `/create-pull-request`). They provide structured, multi-step guidance for common tasks.

### Agents

Agents are specialized sub-agents that handle complex tasks autonomously — like generating analytics dashboards, maintaining architecture docs, or validating Figma designs against implementations.

## Repository Structure

```
claude-plugins/
├── .claude-plugin/
│   └── marketplace.json          # Marketplace catalog
├── plugins/
│   ├── cf-saas-stack/
│   │   ├── .claude-plugin/
│   │   │   └── plugin.json       # Plugin manifest
│   │   ├── rules/                # 15 rules
│   │   ├── commands/             # 7 commands
│   │   └── agents/               # 1 agent
│   └── dev-workflows/
│       ├── .claude-plugin/
│       │   └── plugin.json       # Plugin manifest
│       ├── rules/                # 9 rules
│       ├── commands/             # 11 commands
│       └── agents/               # 6 agents
└── README.md
```

## License

MIT
