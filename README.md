# OpenCode Configuration

A configuration project defining agents, skills, commands, and runtime settings for the OpenCode AI coding assistant.

## Features

- **5 Agents**: architect, deployer, researcher, reviewer, security
- **2 Commands**: `/verify`, `/review` (slash-commands in the TUI)
- **19 Skills**: from brainstorming to systematic debugging
- **7 Plugins**: mem0, railway, vibeguard, wakatime, morph, notifier, oh-my-openagent
- **4 MCP Servers**: context7, gh_grep, github, railway

## Quick Start

```bash
npm install

# Verify configuration (within OpenCode TUI)
/verify

# Review changes (within OpenCode TUI)
/review
```

## Project Structure

```
config/             # Runtime configuration
agents/             # Agent definitions
commands/           # Slash-command definitions
skills/             # Skill definitions (19 skills)
AGENTS.md           # Project knowledge base
opencode.json       # Main runtime configuration
```

## Configuration

See `config/opencode.json` for the full runtime configuration. Provider credentials are loaded from environment variables.

## Contributing

See `CONTRIBUTING.md` for guidelines on adding agents, skills, and commands.
