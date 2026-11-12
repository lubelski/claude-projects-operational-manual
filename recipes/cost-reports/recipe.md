# 18. Routine cost reports

## Problem

Agent work feels cheap and fast, so nobody looks at where the effort goes. The real costs are often not tokens. They are work built before a requirement settled, PRs waiting hours on a permission, and tickets redone. You can't improve what you don't measure. And you shouldn't prescribe fixes before you measure.

## Recipe

Run a routine report that **measures and sets no targets**. It covers three kinds of cost:

1. **Burn:** model tokens, split by area and role.
2. **Compute:** hosted CI minutes, and machine time on build machines.
3. **Flow costs**, the way an engineering org counts them:
   - time blocked, and on whom
   - reopened tickets
   - superseded or thrown-away work (code deleted soon after it landed)
   - abandoned PRs
   - stale statuses
   - untracked work (PRs without tickets)

Sources that worked for us:

| Source | Gives |
|---|---|
| Git history | Line churn by folder, reverts, files added then deleted |
| PR data | Open, merge and close times, abandoned PRs, CI run counts |
| Tracker status history | Reopens, time in each status |
| Thread list | Who is blocked right now (a snapshot only) |
| Claude Code transcripts on a machine | Tokens per message, with the working folder and git branch |

Report shares and trends: this period, last period, and to date. Keep it short, a Library file plus a five-line summary in the project chat. Weekly is a sensible cadence.

## Why it works

It turns hunches into numbers the director can act on, without process nobody asked for. The flow costs usually point at requirements and permissions, not at the agents.

## Pitfalls

- **Cloud thread transcripts vanish with their containers.** Token history from cloud threads is lost unless each thread logs its own usage before it ends. Build-machine transcripts persist on disk.
- **There's no dollar figure on a subscription.** Use tokens and shares.
- **Thread state is a snapshot.** Blocked time needs a daily snapshot, or a read of the messages.
- **The first report finds the expensive lesson.** Ours found that one feature was built and then removed two days later, about 8% of all churn, because its requirement hadn't settled.
