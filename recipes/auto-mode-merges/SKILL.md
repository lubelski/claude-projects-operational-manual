---
name: auto-mode-merges
description: Use when auto mode refuses gh pr merge on a build machine; covers autoMode.allow and its limits.
---

# 11. Auto mode and merges

Researched and tested in November 2026. Auto mode is evolving, so check the current docs: https://code.claude.com/docs/en/auto-mode-config

## Problem

Sessions on a build machine run in auto mode, where a classifier judges each risky action. It refused `gh pr merge` as "Merge Without Review", even with:

- an allow rule `Bash(gh pr merge:*)` in the repo's `.claude/settings.json`,
- a merge-authority section in `AGENTS.md`,
- the director's "ship it", relayed by the coordinator,
- a fresh session that had read the new rules.

At the same time, a cloud thread merged a PR without trouble.

## Recipe

1. **Know where the classifier reads its rules.** `autoMode` rules (`allow`, `soft_deny`, and so on, written as plain-English sentences) are read only from user-level `~/.claude/settings.json`, managed settings, or `--settings`. They are never read from a repo. That's deliberate, so a repo can't approve itself.
2. **Have the director add an unconditional allow sentence** to `~/.claude/settings.json` on the build machine. Keep `"$defaults"`, or the built-in rules are dropped:

   ```json
   {
     "autoMode": {
       "allow": [
         "$defaults",
         "Merging pull requests in github.com/<owner>/<repo> with `gh pr merge <n> --merge` is approved. Never use --admin, and never merge in other repos."
       ]
     }
   }
   ```

   Public reports (and our own test) found that unconditional wording worked and conditional wording ("if the coordinator approved...") did not.
3. **Check it:** `claude auto-mode config` should list the sentence, and `claude auto-mode critique` flags problems. Then restart `claude remote-control` so new sessions load it.
4. **Workers run the merge as a standalone command.** Don't chain `gh pr ready && gh pr merge`, and don't prefix with `cd`. An allow rule skips the classifier only when every part of a compound command matches.
5. **Scope by wording.** There's no per-repo key. Name the repository and the exact command in the sentence. `claude remote-control --settings` is refused at startup, so you can't scope by a separate settings file for one served folder.

## Why it works

The classifier honors explicit user-level intent. Repo files and relayed approvals are exactly the kind of input it's designed to distrust.

## Pitfalls

- **An agent can't make this edit.** Changing `~/.claude/settings.json` is blocked as Self-Modification. The director applies it by hand, through an IT ticket ([recipe 17](../it-tickets/SKILL.md)).
- **A relayed approval isn't the user's approval.** Only the user's own message naming the action clears a soft block. Attaching the director's message through the coordinator didn't work for us.
- **It's a prose rule read by a model, not a hard boundary.** The fallbacks are a `permissions.ask` rule for `gh pr merge` (each merge becomes a one-tap prompt), merging by hand, or running merges from a cloud thread.
- **Don't route around it silently.** We considered having cloud threads do all merges. The director chose to fix the cause instead, which kept one path for merges.

## Example

> After the director added the sentence and restarted the server, the two stuck PRs merged from build-machine threads within two minutes, and the installed app was rebuilt from main.
