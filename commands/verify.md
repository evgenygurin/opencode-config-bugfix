---
description: Validate the OpenCode configuration and referenced assets
agent: reviewer
---

Verify the deployment configuration.

1. Parse `opencode.json` as strict JSON.
2. Verify every configured agent, skill, and command has valid metadata.
3. Check for obvious credential material.
4. Inspect the final diff for stale V1 fields, duplicate configuration, and unnecessary context.
5. Report each executed check and its result.
