# 25. Hygiene without asking

Origin: a second project (cloud threads only, no build machine), November 2026.

Related: [recipe 07](../worktree-hygiene/recipe.md) covers machine-side cleanup. This recipe is about permission for repo-side cleanup.

## Problem

Small cleanup (a stale branch, an outdated tracker description) gets escalated to the director as if it were risky. Each one costs a round trip, and the director ends up clicking delete buttons.

## Recipe

1. **Write a standing order** ([recipe 03](../where-standing-orders-live/recipe.md)): agents may do benign hygiene without asking, such as deleting trivial or stale branches whose work is merged or clearly abandoned.
2. **Guard it:** before deleting a branch, confirm it holds no unmerged work that is still wanted. If it does, report that instead.
3. **Report hygiene in the next summary,** not as its own message.
4. **Turn on "Automatically delete head branches"** in the GitHub repository settings, so merged PR branches clean themselves up.

## Why it works

The director's attention goes to decisions, not chores. The guard keeps the one real risk, losing unmerged work, in check.

## Pitfalls

- **Cloud threads can't delete other branches** (observed November 2026). A thread's git connection may push only to its own working branch, so a delete push is dropped. The GitHub tools available to threads had no branch delete either. Workarounds: automatic head branch deletion for merged PRs, or a session on the director's own machine with their git credentials. Otherwise the director deletes by hand.
- **A "stale" branch may hold intent.** Ours held about 150 lines of tests that never reached main. They targeted an API that no longer existed, so they couldn't be ported. A thread read them, reported what they were meant to prove, and the director chose to rewrite them fresh in a small PR. Read before you delete.
