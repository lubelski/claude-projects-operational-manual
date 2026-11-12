# 08. Account connectors versus machine-local config

Observed in November 2026.

## Problem

Threads on different machines need the same outside tools, such as the issue tracker. It's tempting to add a repo `.mcp.json`, install a CLI with an API key on each machine, or both. Then the config drifts, and cloud threads can't see it.

## Recipe

1. **Prefer account connectors** (claude.ai Settings, Connectors). They follow the account. Cloud threads get them, and so did Remote Control sessions on our build machine, as long as Claude Code there was signed in to the same account. In our test, a reconnect showed up on the machine without a restart.
2. **Use a repo `.mcp.json`** only for tools specific to that repo, versioned with the code.
3. **Avoid per-machine CLIs with their own keys** unless nothing else works. Cloud threads won't have them.
4. **Check which workspace a connector is signed into.** Some trackers authorize one workspace at a time. Pick the right one on the authorize screen, then verify from a fresh thread.

## Why it works

There's one place to manage access, and every thread, cloud or machine, sees the same thing.

## Pitfalls

- **A misfiled workspace.** Our tracker connector was signed in to a personal workspace. The first issues were filed there and had to be re-filed and cancelled by hand, because the connector could no longer see the old workspace after the switch.
- **Old threads may hold an old sign-in.** Verify with a new thread.
- **The coordinator may not use connectors at all.** It delegates connector work to threads, or to a chief of staff ([recipe 04](../chief-of-staff/recipe.md)).
