---
name: pull-requests
description: Use when opening or reviewing an agent-authored pull request; covers template, evidence, and assignees.
---

# 09. The pull request is the artifact

## Problem

Work that lives only in a thread is invisible once the thread ends. Reviewers can't judge a change from "done, tests pass".

## Recipe

Every change ships as a PR, and the PR carries its own evidence.

1. **Use a template.** Ours has four sections: Overview (a TL;DR of the intent), Visual Preview (evidence), Changes (bullets), Notes (surprises, gaps, follow-ups). Keep it in the repo, and point agents to it from `AGENTS.md`.
2. **Evidence comes from the actual change.** UI changes get screenshots or offscreen renders, before and after where useful. Non-visual changes get test output, timings, or logs. Label mocks. Never substitute a design mock for a screenshot.
3. **Name what wasn't verified.** If something can only be tested by hand (hover, drag, focus, a live stream), list it in Notes, and add a line to a manual-test checklist in the repo, so the gap stays visible.
4. **Record the commit you tested.** Put the pushed SHA, build result, and test counts in the PR ([recipe 12](../light-testing/SKILL.md)).
5. **Link the ticket.** Put the ticket ID in the branch name and the PR. Take the number from the tracker, never guess it ([recipe 16](../tickets-express-intent/SKILL.md)).
6. **Open as a draft. Don't assign anyone to a draft.** Add the assignee and reviewer only when the PR is marked ready for review. An assignee on a draft pings a person about work that isn't ready.
7. **Add attribution** for agent-authored PRs, so readers know who asked for the work and which thread made it.

## Why it works

The PR is the one durable place where intent, change, and evidence meet. A reviewer, or a later agent, can judge it without the thread.

## Pitfalls

- **Images in a private repo.** Links to raw files in a private repo don't render. Upload images as PR attachments instead of committing them.
- **Offscreen renders can't show interaction.** Say so.
- **"No ticket" PRs.** When the tracker was unreachable, our PRs went out without tickets. File them afterward, so the board stays the source of truth.
