# Agent Commands

Shared command definitions for AI coding agents (Claude Code, Opencode). This repo contains reusable prompt templates that guide agent behavior for common development workflows.

Each `.md` file in `commands/` is a standalone instruction set that can be invoked via `/command-name` inside the agent session.

## Syncing

Run `npm run sync` to copy all commands to both Claude and Opencode:

```
~/.claude/commands/
~/.config/opencode/commands/
```

The sync also runs automatically on `npm install` via the `prepare` lifecycle hook.

## Adding a Command

1. Add a new `.md` file to `commands/`
2. Run `npm run sync`

**⚠️ Caution: Avoid overlapping commands.** Before adding a new command, review the existing commands below to ensure the scope doesn't overlap with an existing one. If a command name or description is too similar to another, the agent may invoke the wrong one ambiguously.
