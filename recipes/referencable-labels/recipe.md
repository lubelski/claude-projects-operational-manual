# 19. Referencable labels

Origin: a second project (cloud threads only, no build machine), November 2026.

Overlaps [recipe 01](../director-manager-ics/recipe.md), rule 2, which labels decision options. This recipe applies the same idea to every list, not only decisions.

## Problem

The director replies from a phone, between other work. "The second thing you said about the branch" is slow to type and easy to misread. Bullet lists give the director nothing short to point at.

## Recipe

Label every list item in chat with a short tag the director can type back.

1. **Use brackets.** `[A]`, `[B]` for top-level topics, such as agenda items. `[1]`, `[2]` for points inside one message. `[a]`, `[b]` for options inside a point.
2. **Keep a tag stable while it's live.** Agenda item `[C]` stays `[C]` across messages and days, until it closes. Don't re-letter a list because one item finished.
3. **Use the tags yourself.** "Next up is [C]" and "waiting on you: [4]" let the director follow without rereading.
4. **Put the rule in memory or project instructions**, so a new coordinator keeps doing it.

## Why it works

A two-character reply carries a whole decision. Stable tags also give the conversation a shared index that survives across days.

## Pitfalls

- **Two tag schemes in one message collide.** If `[A]` to `[F]` already name agenda items, label options inside a message `[1]`, `[2]` or `[a]`, `[b]`, not `[A]`, `[B]`.
- **Numbers restart in every message.** "[2]" alone is ambiguous after a few messages. Top-level tags (letters) should be the ones that persist.

## Example

> **Director:** let's do [1] for the trigger, and park [C].
