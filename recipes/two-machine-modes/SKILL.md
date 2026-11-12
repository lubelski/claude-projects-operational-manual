---
name: two-machine-modes
description: Use when adding a machine to the project; classifies it as an autonomous build machine or a personal machine.
---

# 05. Two machine modes

## Problem

Cloud threads run in Linux containers. They can't build or run apps that need another OS, such as a Mac app with Xcode. So you bring real machines into the project. Without a clear rule, an agent may treat the director's laptop like a build server, or a build server like a laptop.

## Recipe

Classify each machine by what agents may change on it, not by its name.

| | **Autonomous build machine** | **Personal machine** |
|---|---|---|
| Purpose | Agents build, test, and run dev builds on their own | The director's own machine. They use the app here. |
| Agents may | Create worktrees, build, run tests, install the reference copy of main, launch dev builds, install tools they need | Only what the director asks for in that request |
| Default device for new threads | Yes | No |
| Typical state | Default checkout on latest main; latest main installed as a reference copy | Whatever the director keeps there |

Rules:

1. Write the repo's machine guidance by mode: "on an autonomous build machine...", "on a personal machine...". Never name a specific machine or path. More machines will come online in either mode.
2. Keep the project's default device on the build machine, so feature threads land there without a prompt.
3. Get builds to the personal machine by **pull**, not by agents reaching into it ([recipe 13](../pull-based-test-builds/SKILL.md)).

## Why it works

The mode is the permission boundary. A new machine needs only its mode to be known, and every rule follows from it. Generic docs survive hardware changes.

## Pitfalls

- **Cloud threads can still do a lot**: edit code, run Linux-compatible tests and scripts, open and merge PRs, and use connectors. Only send work to a machine when it needs that machine.
- **A dev build and the installed copy must not collide.** Give dev builds their own app identifier and display name, so settings and data stay separate and both can run at once. Never replace an installed copy while it runs. Quitting it may kill the director's live work.
- **Killing by process name kills every copy.** Stop a dev build by matching its path.
- **Package or toolchain setup on a fresh worktree can be slow.** We measured about 10 minutes the first time. Reuse caches across worktrees where the tool allows it.

## Example

> Repo guidance, `docs/workstation.md`: "On an autonomous build machine, keep the default checkout on main and the installed app at latest main. Work in a worktree. On a personal machine, change nothing beyond the request."
