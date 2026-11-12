# 06. Connecting a machine with Remote Control

Behavior observed in November 2026. Check current docs, since this changes.

## Problem

The coordinator can only start threads on machines it can see. The first attempts to connect a machine often fail quietly: the machine never appears, or the wrong folder appears.

## Recipe

1. On the machine, sign in to Claude Code with the same account as the project.
2. From a shell, `cd` into the repo checkout and run `claude remote-control`. Leave it running. This "serves" that folder, so the project can start new sessions there.
   - Running `/remote-control` *inside* a chat session shares only that one session. It doesn't register the folder for new sessions.
3. Pick a spawn mode when asked:
   - **worktree**: each session gets its own git worktree inside the repo (`.claude/worktrees/<name>`). This is our default ([recipe 07](../worktree-hygiene/recipe.md)).
   - **same-dir**: sessions share the checkout. Use this only if you manage worktrees yourself.
4. Ask the coordinator to list devices. The machine and folder should now appear.
5. Approve the first folder card. Approving a card also makes that device the project's **default**, and only the default skips the card next time. Keep the default on the build machine.
6. To set the permission mode for spawned sessions, pass `--permission-mode` to `claude remote-control`. `--settings` is refused at startup (observed November 2026).

## Why it works

Serving a folder from a long-running process lets the project start fresh, isolated sessions on demand, with the machine's real toolchain and credentials.

## Pitfalls

- **A stray served folder.** The first machine we saw was serving an unrelated folder, because that's where Claude Code happened to be running. Serve the repo you want.
- **Two machines with the same path look identical** on approval cards. Approving one moves the default to it. Expect to re-approve when you switch.
- **The thread's machine stops when the process stops.** If `claude remote-control` exits, the threads there go quiet. Run it in a terminal multiplexer or a launch agent on the build machine.

## Example

```
~/dev/myapp (main) $ claude remote-control
Spawn mode for this project:
  [1] same-dir   [2] worktree
Choose [1/2]: 2
```
