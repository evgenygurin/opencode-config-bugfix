# Contributing to OpenCode Configuration

## Getting Started

1. Clone this repository
2. Install dependencies: `npm install`
3. Edit configuration files in `config/`, `agents/`, `commands/`, or `skills/`

## Project Structure

```
config/             # Runtime configuration (opencode.json)
agents/             # Agent definitions
commands/           # Slash-command definitions
skills/             # Skill definitions (one SKILL.md per directory)
```

## Adding a New Agent

1. Create `agents/<name>.md` with YAML frontmatter:
   ```yaml
   ---
   description: Short description of the agent
   mode: subagent
   permission:
     edit: deny
     bash: ask
   ---
   ```
2. Add the agent to `config/opencode.json` `fallback.agents` section

## Adding a New Skill

1. Create `skills/<name>/SKILL.md` with YAML frontmatter:
   ```yaml
   ---
   name: <skill-name>
   description: What this skill does
   compatibility: opencode
   ---
   ```
2. Add a `## Dependencies` section documenting prerequisites
3. Keep the skill focused and actionable

## Adding a New Command

1. Create `commands/<name>.md` with YAML frontmatter:
   ```yaml
   ---
   description: What this command does
   agent: <agent-name>
   ---
   ```

## Validation

Before committing, run these checks:

- All frontmatter fields are present
- `config/opencode.json` is valid JSON
- No secret values are committed
- Provider credentials use `{env:VAR_NAME}` syntax

## Rules

- Never hardcode API keys or credentials
- Never create competing runtime configs
- Never modify files without updating YAML frontmatter
- Never commit secret values, even in comments
