# 03. Where standing orders live

## Problem

A rule the director gave once in chat is forgotten by the next thread. Some rules get written to project memory, some to the repo, and some nowhere. Nobody can say which rule wins or which reader sees which.

## Recipe

Know the two kinds of automation and the three places to write rules.

**Two kinds of automation**

- **Mechanical:** a hook, a cron job, a CI check, a permission setting. It is guaranteed, and it runs whether or not a model agrees.
- **Procedural:** a model reads a note and chooses to act on it. It works more like habit or policy than automation. We call these **standing orders**. How reliably one is followed depends on how often it is read and how clearly it is worded.

**Three places for standing orders, strongest first**

| Place | Who reads it | Put here |
|---|---|---|
| **Project instructions** (project settings) | Every coordinator and every thread, at start | How the director wants to work: the operating model, escalation format, merge authority, approval rules. The director owns this text. |
| **Repo docs** (`AGENTS.md`, `CLAUDE.md`, docs) | Agents working in the code, in any project or none | How to work in this codebase: build, test, PR format, the worker side of merge rules. |
| **Project memory** | The coordinator and threads, as recalled notes | Facts and decisions: which machine does what, ticket numbers, what was tried. The coordinator keeps it current. |

Rules of thumb:

- If it is a **rule**, put it in project instructions. If it is a **fact**, put it in memory.
- Policies that workers must apply go in both places: the policy in project instructions, and the worker's procedure in repo docs.
- Anything that has to hold even if a model disagrees needs a mechanical control, not a note.

## Why it works

Each reader gets the rule from the place it actually reads. Separating rules from facts keeps authority clear. Memory is the coordinator's notebook, and the director's rules shouldn't depend on how the coordinator worded a note.

## Pitfalls

- **The coordinator has a built-in standing order to save what it learns.** That's useful, but it decides what counts and how to word it. Promote anything you consider a rule into project instructions.
- **Agents usually can't edit their own rules.** Some safety modes block an agent from changing `AGENTS.md`, skills, or settings as "self-modification". Plan for the director to land those changes ([recipe 17](17-it-tickets.md)).
- **Docs don't move safety checks.** A permission classifier that runs in the agent's session judges each action itself. Writing "merges are allowed" in the repo did not change its mind ([recipe 11](11-auto-mode-merges.md)).

## Example

The director asks: "should these orders live in memory, the repo, or project notes?" The answer: the merge policy goes in project instructions (the coordinator gives the director a paste-in snippet). The worker procedure goes in `AGENTS.md` through a PR that the director approves. Memory gets a pointer to both.
