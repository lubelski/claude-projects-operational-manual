---
name: chief-of-staff
description: Use when the coordinator lacks repo or tracker tools and needs a long-lived thread to read the code and board for it.
---

# 04. A chief-of-staff thread

## Problem

The coordinator may have no repo, GitHub, or tracker tools of its own. Everything it knows about the code and the backlog then comes from worker reports. That's a narrow pipe. Plans rest on hearsay, and drift goes unnoticed. In our case, the coordinator didn't know the CI never built the app, or that a third of the board's statuses were stale.

## Recipe

Start one long-lived cloud thread as the coordinator's **chief of staff**. Give it the repo and the tracker connector. Its main output is a set of files in the project Library, which the coordinator can read directly.

1. The coordinator starts the thread with a brief:
   - Study the codebase, and write `cos/codebase.md`: an architecture map with file paths, the main flows, where common changes go, sharp edges, and conventions.
   - Read the tracker, and write `cos/board.md`: every open issue with ID, status, a one-line gist, dependencies, and an estimate of size and risk. Add recent closures and open PRs.
   - Write `cos/briefing.md`: one page covering what matters now, what's blocked and on whom, and next work split into IC-sized tasks.
2. Don't let the chief of staff take on feature work, and don't let it edit the tracker unless asked.
3. Afterward, the coordinator sends it questions ("where does X live?", "is ticket N done?") and refresh requests. The thread keeps the files current.
4. Use it for side jobs that need reading across the codebase or tracker: research, design write-ups, cost reports, this manual.

## Why it works

Files are a wide pipe. The coordinator reads the full map itself instead of a summary of a summary. The chief of staff has the context to judge drift, because it read both the code and the board. In VSM terms, it is System 3*: an audit channel that doesn't go through the operational units.

## Pitfalls

- **The first pass finds real problems.** Ours found that "merge when CI passes" was an empty rule (CI built nothing), that several tickets looked done but were still open, and that a PR was stacked on another PR's branch. Budget time to act on the findings.
- **Keep the files dense, not long.** The reader is a manager judging and splitting work, not a newcomer.
- **Library paths are shared.** Other threads write there too. Use a subfolder (`cos/`), and re-read a file before you change it.
- **A long-lived thread loses its container's local state between sessions.** Keep anything durable in the Library or in memory, not in its scratch space.

## Example brief

```
You are the coordinator's long-lived chief of staff, in a cloud thread with
the repo and the tracker connector. The coordinator can read the project
Library but has no repo or tracker tools, so your main output is Library files.
1. Write cos/codebase.md ...
2. Write cos/board.md ...
3. Write cos/briefing.md ...
Then stay available for questions and refreshes. Don't take on feature work,
and don't edit tracker issues without being asked.
```
