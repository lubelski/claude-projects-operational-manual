# 14. Stacked PRs and merge order

## Problem

A follow-up PR is often built on an unmerged PR's branch. Its base is then that branch, not main. If the first PR merges in an unexpected way, the second shows duplicate commits or conflicts, or targets a branch that no longer exists.

## Recipe

1. **Say it in the PR.** The first line of the stacked PR's Overview reads "Stacked on #N; merge #N first."
2. **Merge in order.** The coordinator gives the order explicitly: "#101, then #102, then #103 after it's retargeted."
3. **After the base merges,** rebase the stacked PR onto main, retarget its base to main, re-run the build and tests, and update the SHA in the PR.
4. **Delete the merged branch.** GitHub retargets dependents automatically when the base branch is deleted on merge.

## Why it works

Stacks let work continue without waiting for review. Explicit order and a rebase step keep them from turning into surprise conflicts.

## Pitfalls

- **Squash merges rewrite the base.** The stacked PR then shows the base's changes again until it's rebased.
- **The chief of staff should flag stacks** on the board, since a PR list doesn't make them obvious ([recipe 04](04-chief-of-staff.md)).
- **Each rebase voids the attestation.** Test again on the new SHA.
