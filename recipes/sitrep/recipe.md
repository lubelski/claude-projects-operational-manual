# 21. Sitrep

Origin: a second project (cloud threads only, no build machine), November 2026.

Related: the example in [recipe 01](../director-manager-ics/recipe.md) ("What's blocked on me right now?") is the narrower version of the same habit.

## Problem

The director comes back after a few hours. Scrolling the project chat to rebuild the state of the work is slow, and thread cards show activity, not meaning.

## Recipe

When the director asks for a **sitrep** (situation report), the coordinator answers with four short headings, in this order:

1. **Shipped:** merged PRs and closed items since the last sitrep, with links.
2. **Waiting on you:** each ask, with the exact action and a link. This is the part the director acts on.
3. **In flight:** open PRs and working threads. Say "nothing in flight" when that's true.
4. **Agenda remaining:** the open items of the stored agenda ([recipe 20](../stored-agenda/recipe.md)), one line each.

Label every line ([recipe 19](../referencable-labels/recipe.md)), so the director can answer "[4] yes, [5] every 10".

## Why it works

The director gets the whole state in one screen, and the asks are separated from the news. A fixed shape also makes gaps visible. An empty "waiting on you" means the project isn't blocked on them.

## Pitfalls

- **It's on request, not on a timer.** A scheduled sitrep becomes noise when nothing changed. [Recipe 18](../cost-reports/recipe.md) is the routine report.
- **Don't pad it.** If nothing shipped, say so in one line.

## Example

> **Shipped**
> [1] Versioned actor identity, PR #8 merged.
> [2] Five credential tests, PR #9 merged.
>
> **Waiting on you**
> [3] Delete the leftover branch on the branches page.
> [4] Pick the retrospective trigger. My proposal is every 5 merged PRs.
>
> **In flight:** nothing.
>
> **Agenda remaining:** [C] concurrent writers, [D] backlog order, [E] no CI.
