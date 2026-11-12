---
name: shared-tracker-login
description: Use when every agent and the director share one issue-tracker login; owner goes in the title prefix.
---

# 15. One shared tracker login

## Problem

Every agent and the director reach the issue tracker through one connector, so every issue shows the same creator and assignee. You can't tell from the tracker who owns what.

## Recipe

Put the owner in the title as a prefix:

- `<Director's name> | ` for the human, such as `Dana | `
- `Project Manager | ` for the coordinator
- `Worker {ID} | ` for a thread, where `{ID}` is something the thread can name itself by, such as its branch or a short slug

For example: `Dana | Add the merge rule on the build machine`, or `Worker input-box | Fix scrollbar inset`.

Leave ordinary product tickets, the ones that express intent ([recipe 16](../tickets-express-intent/SKILL.md)), without a prefix until someone owns them.

Write the convention into project memory, or better, the project instructions, so every thread follows it.

## Why it works

It needs no tracker configuration, it survives connector changes, and the owner shows in every list, search result, and link preview.

## Pitfalls

- **Changing owners means renaming the issue.** Do it. It's cheap.
- **Agents may forget the prefix** if the rule is only in memory. If it keeps happening, promote it to project instructions.
