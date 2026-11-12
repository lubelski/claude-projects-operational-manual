# 20. A stored agenda, walked one item at a time

Origin: a second project (cloud threads only, no build machine), November 2026.

## Problem

A first survey of a repo or a backlog turns up eight things at once. Dumped into chat, they bury each other. The director answers the easiest one, and the rest scroll away. Questions that were already deferred come back, because nothing records that they were deferred.

## Recipe

1. **Keep the agenda in project memory**, not only in chat. Each item gets a stable letter ([recipe 19](../referencable-labels/recipe.md)), a one-line description, and a state.
2. **Walk it one item at a time.** Raise the current item, settle it, then name the next one: "[A] is done. Next up is [B]."
3. **Add new findings as new items** instead of raising them on the spot. "No CI (continuous integration) on the repo. Added to the agenda as [E]."
4. **Record what was deferred, inside the item.** Write "deferred, do not foreclose, do not ask" next to each deferred question. Close the item with the date and the outcome (PR, ticket).
5. **Never ask about a deferred question.** Re-raise it only when the director brings it back.

## Why it works

The director sees one decision at a time, with context. The agenda in memory survives across threads and coordinator restarts, so nothing is lost when a topic is set aside. It is also a ready-made sitrep ([recipe 21](../sitrep/recipe.md)).

## Pitfalls

- **Deferred questions creep back in a new shape.** In our case the coordinator deferred a design hook, then asked two follow-up questions that only mattered if the hook existed. The director had to say "it sounds like you're asking about a question we just deferred." Before asking, check whether the question depends on something deferred.
- **Memory files have a size limit.** Keep closed items to one line, and move detail into the PR or ticket.
- **One item at a time is a default, not a rule.** Small, independent items can be batched into one message, as [recipe 02](../escalations/recipe.md) suggests for asks.

## Example

```
## Agenda (walk one item at a time)
- [A] Identity model. DONE 2026-11-11, PR #8. Deferred, do not ask: nesting; outside definition hook.
- [B] Leftover branch. DONE, tests rewritten in PR #9.
- [C] Concurrent writers untested. Next.
- [D] Backlog order.
```
