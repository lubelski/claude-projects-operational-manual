---
name: worktree-hygiene
description: Use when several agents share a machine; covers the default checkout, per-task worktrees, and cleanup.
---

# 07. Worktree hygiene

## Problem

Several agents on one machine will trip over each other in a single checkout. Left alone, worktrees pile up, the default checkout drifts off main, and nobody knows which build is the "real" one.

## Recipe

1. **The default checkout stays on latest main.** Agents never work in it. After a merge, the merging agent pulls main into it.
2. **Every task runs in its own worktree.** The simplest route is Remote Control's native worktree spawn mode, where each session gets `.claude/worktrees/<name>`. A worktree manager (for example a `.wt/` folder of named or pooled worktrees) is fine for extra worktrees.
3. **Ignore worktree folders in git.** Add `/.claude/worktrees/` (and `.wt/` if used) to the repo's `.gitignore`, or to a global gitignore on the machine.
4. **Keep latest main installed as a reference copy** on the build machine. Rebuild it after each merge, so "what's on main" is always something you can run.
5. **Clean up after the feature session.** When a PR merges, the agent removes its worktree and local branch, and deletes the remote branch if the merge didn't.
6. **Consider pooled worktrees only when numbers justify them.** We measured cold builds at about a minute after the first package fetch. That wasn't enough to justify a pool. Measure before adding one.

## Why it works

Isolation prevents agents from colliding. A clean main checkout plus an installed reference copy gives everyone the same baseline. Cleanup keeps the machine from filling up and keeps `git worktree list` readable.

## Pitfalls

- **Untracked worktree folders show up in `git status`** in the default checkout until they're ignored.
- **The first dependency fetch in a fresh worktree can be very slow.** Point the build tool at an existing package cache where it supports that.
- **Merged branches linger on the remote** if the merge doesn't delete them. Check after merging.

## Example

> After merge: `git -C <default checkout> pull --ff-only`, rebuild and reinstall the reference app, then remove the worktree.
