# OpenCode Project Knowledge Base

**Generated**: 2026-09-11
**Commit**: N/A
**Branch**: N/A

## OVERVIEW

OpenCode configuration project — defines agents, skills, commands, and runtime configuration for the OpenCode AI coding assistant. Primarily configuration-driven with no traditional source code.

## STRUCTURE

```
opt/opencode/opencode/
├── AGENTS.md              # This file — project knowledge base
├── config/                # Config directory (opencode.json lives here)
│   └── opencode.json      # Canonical runtime configuration
├── opencode.json          # Symlink to config/opencode.json
├── package.json           # Dependencies (@opencode-ai/plugin)
├── tui.json               # TUI plugin configuration
├── .gitignore             # Excludes node_modules, lock files
├── agents/                # Agent definitions (5 agents)
│   ├── architect.md
│   ├── deployer.md
│   ├── researcher.md
│   ├── reviewer.md
│   └── security.md
├── commands/              # Command definitions (2 commands)
│   ├── review.md
│   └── verify.md
└── skills/                # 19 skill directories, each with SKILL.md
    ├── brainstorming/
    ├── dispatching-parallel-agents/
    ├── executing-plans/
    ├── finishing-a-development-branch/
    ├── gitnexus/
    ├── receiving-code-review/
    ├── repo-research/
    ├── requesting-code-review/
    ├── security-review/
    ├── subagent-driven-development/
    ├── superpowers/
    ├── systematic-debugging/
    ├── test-driven-development/
    ├── using-git-worktrees/
    ├── using-superpowers/
    ├── verification/
    ├── verification-before-completion/
    ├── writing-plans/
    └── writing-skills/
```

## WHERE TO LOOK

| Task | Location | Notes |
|------|----------|-------|
| Runtime config | `config/opencode.json` | Providers, plugins, MCP servers, permissions, fallback models |
| Agent definitions | `agents/*.md` | YAML frontmatter with description, mode, permissions |
| Skill definitions | `skills/*/SKILL.md` | YAML frontmatter with name, description, compatibility |
| Command definitions | `commands/*.md` | YAML frontmatter with description, agent reference |
| TUI config | `tui.json` | Plugin registration |
| Dependencies | `package.json` | Single dep: @opencode-ai/plugin |

## CROSS-REFERENCES

| Agent | Commands | Skills | Permissions |
|-------|----------|--------|-------------|
| `architect` | — | brainstorming, writing-plans | edit: deny, bash: ask |
| `deployer` | — | executing-plans, finishing-a-development-branch | railway_*: ask |
| `researcher` | repo-research, websearch | websearch, webfetch, context7_* | github_*: ask |
| `reviewer` | review, verify | receiving-code-review, requesting-code-review | github_*: ask |
| `security` | — | security-review | websearch, webfetch |

## CONVENTIONS

- All definition files use YAML frontmatter (`---` delimited) with `description`, `mode`, `permission` or `compatibility` fields
- Agent files define `mode: subagent` with granular permission controls (edit: deny, bash: ask, etc.)
- Skill files always have `compatibility: opencode` and a `name`/`description` pair
- Skill files include a `## Dependencies` section documenting prerequisites
- Command files reference an agent via the `agent:` field
- Provider credentials use `{env:VAR_NAME}` syntax in config/opencode.json — never hardcode secrets
- All agents reference `openrouter/cohere/north-mini-code:free` as the default model
- Config files live in `config/` directory; `opencode.json` is a symlink to `config/opencode.json`

## VALIDATION

Run these checks before committing:

```bash
# Validate opencode.json is valid JSON
cat config/opencode.json | python3 -m json.tool > /dev/null

# Verify all agent files have required frontmatter
for f in agents/*.md; do grep -q "^description:" "$f" && grep -q "^mode:" "$f"; done

# Verify all skill files have required frontmatter
for f in skills/*/SKILL.md; do grep -q "^name:" "$f" && grep -q "^compatibility:" "$f"; done

# Verify all command files have required frontmatter
for f in commands/*.md; do grep -q "^description:" "$f" && grep -q "^agent:" "$f"; done
```

## ANTI-PATTERNS

- Never hardcode API keys or credentials in opencode.json — always use `{env:VAR_NAME}`
- Never create competing runtime configs — `opencode.json` is the single source of truth
- Never modify agent/command/skill files without updating their YAML frontmatter
- Never commit secret values, even in comments
- Never expose agent bash permissions broadly — use granular `ask`/`allow`/`deny`

## UNIQUE STYLES

- Configuration-only project: no source code, no tests, no CI/CD files
- Plugin-based architecture: 7 plugins loaded (mem0, railway, vibeguard, wakatime, morph, notifier, oh-my-openagent)
- 4 MCP servers configured: context7, gh_grep, github, railway
- Permission model is declarative and granular per-agent

## COMMANDS

```bash
# Install dependencies
npm install

# Verify configuration (slash-command inside the OpenCode TUI)
/verify

# Review changes (slash-command inside the OpenCode TUI)
/review
```

> **Note**: `verify` and `review` are slash-commands invoked as `/verify` and `/review` within the OpenCode TUI — they are not CLI subcommands. Running `opencode verify` in the terminal treats `verify` as a project path and will fail.

## NOTES

- The `fallback` section maps each agent to a specific model
- `compaction` is enabled with auto-prune (reserved: 10000 tokens, tail_turns: 15)
- `snapshot: true` enables session snapshots
- `share: "disabled"` prevents session sharing
- The `@morphllm/opencode-morph-plugin` is included for morph capabilities
- `railway_*` and `github_*` permissions are scoped to `ask` mode