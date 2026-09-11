# Agents Domain

**Reason**: Distinct domain with 5 specialized agent definitions.

## OVERVIEW

5 agent definitions for specialized AI coding assistant roles. All agents use `mode: subagent` with granular permission controls.

## STRUCTURE

```
agents/
├── architect.md
├── deployer.md
├── researcher.md
├── reviewer.md
└── security.md
```

## WHERE TO LOOK

| Task | Location |
|------|----------|
| Add a new agent | `agents/<name>.md` |

## CONVENTIONS

- Every agent file uses YAML frontmatter with: `description`, `mode`, `permission`
- All agents have `mode: subagent` and `edit: deny` by default

## ANTI-PATTERNS

- Never give an agent `edit: allow` unless explicitly required