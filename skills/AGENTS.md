# Skills Domain

**Reason**: Distinct domain with 19 skill directories, each defining reusable workflows.

## OVERVIEW

19 skill definitions, each a self-contained workflow module. All skills have `compatibility: opencode`.

## STRUCTURE

```
skills/
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

| Task | Location |
|------|----------|
| Add a new skill | `skills/<name>/SKILL.md` |
| Modify skill instructions | `skills/<name>/SKILL.md` |

## CONVENTIONS

- Every skill directory contains exactly one `SKILL.md`
- YAML frontmatter must include: `name`, `description`, `compatibility: opencode`

## ANTI-PATTERNS

- Never duplicate skill functionality across multiple SKILL.md files
- Never add a skill without updating the `name`/`description` frontmatter