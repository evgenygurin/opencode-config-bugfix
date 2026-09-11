---
name: systematic-debugging
description: Debug issues using a systematic approach
compatibility: opencode
---

# Systematic Debugging

1. Reproduce the issue.
2. Identify the root cause by isolating variables.
3. Form a hypothesis and test it.
4. Fix the root cause, not the symptom.
5. Verify the fix doesn't introduce regressions.
6. Document the fix and the debugging process.

## Dependencies

- No external dependencies. This skill is built into OpenCode.
- Requires: OpenCode runtime with `compatibility: opencode`.

Prefer reading source code over guessing. Use logging and diagnostics before proposing changes.