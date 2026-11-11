# 16. Tickets express intent

## Problem

Agents tend to rewrite a ticket to match what they built. The original intent is lost, and nobody can tell whether the work met it. Agents also guess ticket numbers when naming branches, and the guesses are wrong.

## Recipe

1. **A ticket states intent:** the problem, the desired experience, and the constraints, ideally with reference material. The director writes it, or it's written with them.
2. **Sub-issues track implementation.** Create them under the intent ticket as the work reveals concrete steps, at any point. Keep each small and verifiable. Update status as work lands, and link the PR.
3. **Never rewrite intent to match the build.** Record divergence in a comment, or ask the director. If the intent itself changes, that's a conversation, not an edit.
4. **Close the parent only when the intent is satisfied.** Leftover or discovered work becomes new sub-issues.
5. **Take the number from the tracker before you name the branch.** Create or find the ticket first. We had two guessed numbers go wrong in two days, and each cost a rename of the branch, the worktree, and code comments.
6. **Put agent detail in a collapsible section** at the end of the description ("Agent notes"), so the human-readable part stays short.

## Why it works

Intent stays stable and reviewable while implementation detail grows underneath it. The tree of sub-issues shows how much work the intent really took.

## Pitfalls

- **Statuses drift.** Sub-issues get implemented with no PR link, and parents stay "In Progress" after everything shipped. A periodic hygiene pass by the chief of staff ([recipe 04](04-chief-of-staff.md)) keeps the board trustworthy. Get the director's OK before bulk edits.
- **Product questions block tickets quietly.** When a ticket needs a product call, say so in the ticket and in the coordinator's next decision list.
