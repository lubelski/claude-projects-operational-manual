# 17. IT tickets for the human

## Problem

Some changes only a human can make: permission settings, an agent's own rules, `sudo` fixes on a machine, account connectors, approvals on another device. If these arrive as scattered chat messages, they get lost, and the work behind them stalls without anyone noticing.

## Recipe

When work needs a step agents may not or cannot take, the coordinator files a ticket for the director, "by the book", and sends the link.

1. **The title** uses the director's prefix ([recipe 15](15-shared-tracker-login.md)): `Director | <what to do>`.
2. **The description** is a checklist the director can work through without context:
   - each item is a checkbox, with the exact command, file, or snippet
   - what each item unblocks, such as which PRs
   - a "done when" line for each item, so anyone can verify it
3. **Include a paste-in prompt** when the change is to agent rules. The director can paste it into a Claude Code session in a non-auto permission mode and approve each edit as it comes up. Also attach a patch file in the Library as a fallback.
4. **Keep one standing IT ticket** for small items, and give large ones their own.
5. **When the director says "done", verify** by retrying the blocked step, then tick the box.

Typical items:

- Allow rules for `gh pr ready` and `gh pr merge` in the repo's agent settings.
- An `autoMode.allow` sentence in the build machine's user settings ([recipe 11](11-auto-mode-merges.md)).
- Changes to `AGENTS.md`, skills, or settings, which agents can't commit themselves.
- Fixing package-manager permissions on a machine.
- Reconnecting a connector to the right workspace.
- Cancelling issues in a workspace the connector can no longer see.

## Why it works

The director gets one place to look, can batch the work, and every item has a test. Blockers become visible on the board instead of hiding in threads.

## Pitfalls

- **Agents are blocked from loosening their own permissions, and should be.** Don't look for workarounds. Write the ticket.
- **The ticket can be filed in the wrong place** if the connector is pointed at the wrong workspace. Re-file it, and cancel the stray copy by hand.
