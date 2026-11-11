# 10. Merge authority as standing orders

## Problem

"Don't merge without the user's authorization" makes the director the bottleneck for every one-line fix. "Merge when CI passes" is empty if CI doesn't build the product. The project needs a rule for who may merge what.

## Recipe

Split PRs by risk, and write the rule twice: the policy in project instructions, and the worker's procedure in repo docs.

**Policy (project instructions):**

```
## Merge authority (standing orders)
- Every PR gets a risk assessment from the worker, confirmed by the coordinator.
- Low risk: the coordinator's approval is enough. The worker marks it ready
  and merges once the build and tests pass on the pushed commit, with the SHA
  and results in the PR.
- Higher risk: escalate to the director. Either the worker or the coordinator
  can call a PR higher risk, and either one is enough. Higher risk includes:
  - migrations of saved user data or settings
  - changes to an external protocol or process lifecycle
  - UI behavior that only a person can test (windows, drag, focus)
  - dependency changes
  - deleting or rewriting large areas
  - changes to agent rules (AGENTS.md, CLAUDE.md, skills, settings)
  - anything the worker is unsure about
- Every escalation says what the change does, the evidence, the risk, and why
  it needs the director.
- If main breaks, revert first. A revert needs no approval.
```

**Worker procedure (`AGENTS.md`):**

1. State the risk (low or higher) and why, in the PR's Notes.
2. For low risk, once the build and tests pass on the pushed commit, post a PR comment with: the risk call, the coordinator's approval (quoted, with its time), and the SHA with build and test results.
3. Mark the PR ready, merge it as a standalone command ([recipe 11](11-auto-mode-merges.md)), then pull main into the default checkout.
4. For higher risk, escalate and do not merge.

## Why it works

Most changes are low risk and move at agent speed. The director's attention goes to the changes that deserve it. Either party can raise the bar, which keeps judgment conservative. The merge comment leaves an audit trail on the PR itself.

## Pitfalls

- **Changes to agent rules always need the director.** It's also often mechanically enforced: agents can't commit edits to their own rules ([recipe 03](03-where-standing-orders-live.md)). File it as a ticket for the director ([recipe 17](17-it-tickets.md)).
- **Writing the policy doesn't grant the permission.** A session's safety classifier may still refuse the merge. That's [recipe 11](11-auto-mode-merges.md).
- **Allow `gh pr ready` and `gh pr merge` in the repo's agent settings**, or the worker will stop at a permission prompt.
