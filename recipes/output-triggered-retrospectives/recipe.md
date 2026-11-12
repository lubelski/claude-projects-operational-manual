# 23. Retrospectives triggered by output

Origin: a second project (cloud threads only, no build machine), November 2026.

Related: [recipe 18](../cost-reports/recipe.md) measures costs on a calendar. This recipe looks at roles, and is triggered by output.

## Problem

Agent work is spiky in wall-clock time. A week can hold twenty merges or none, so a biweekly retrospective is either late or empty. Meanwhile roles drift. A long-lived thread quietly takes on a second job, and nobody notices until it's doing both badly.

## Recipe

1. **Trigger on output, with a count.** We chose every 10 merged PRs. The coordinator keeps the count in project memory and tells the director when one is due.
2. **Add early triggers for clear signals:**
   - a PR sent back twice
   - a thread that stalls
   - one agent doing two distinct jobs
3. **What the retrospective does:** read what each thread was asked and what it did. Report role overlap, repeated friction, and any case for a new persistent agent (or for retiring one).
4. **Recommend, don't restructure.** The director decides whether to add or split agents.

Options we considered for the trigger:

| Trigger | Upside | Downside |
|---|---|---|
| Merged PRs | Tracks shipped work, easy to count | Rewards splitting PRs |
| Lines changed | Scales with effort | Rewards churn, misses research and review |
| Threads finished | Counts non-code work | Threads vary hugely in size |
| Signals | Fires when something is wrong | Silent when drift is slow |
| Calendar backstop | Guarantees a floor | Spiky work makes it noisy |

## Why it works

Retrospectives land after a similar amount of work each time. The signal triggers catch problems the count would reach too late.

## Pitfalls

- **Every proxy for "meaningful progress" is a little off.** The director chose merged PRs knowing that, because they also wanted PRs kept small. Small PRs make the count climb faster, so pick N with your PR size in mind.
- **Thread transcripts may vanish** with their containers ([recipe 18](../cost-reports/recipe.md)). The retrospective reads what survives: thread messages, PRs, and memory.
