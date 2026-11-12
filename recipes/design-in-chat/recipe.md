# 22. Design in chat, then build

Origin: a second project (cloud threads only, no build machine), November 2026.

Related: [recipe 16](../tickets-express-intent/recipe.md) (intent tickets) and the over-design pitfall in [recipe 12](../light-testing/recipe.md).

## Problem

A design question handed straight to a build thread comes back as a large PR built on the agent's guesses. A design question handed to the director as a long survey comes back unanswered, because it asks too much at once.

## Recipe

1. **Ask what the domain fixes before proposing a design.** Does the problem point at one solution, or at several avenues with tradeoffs? Lay out the avenues in labeled form ([recipe 19](../referencable-labels/recipe.md)), with a lean.
2. **Let the director reframe.** Their answer often replaces your framing. Restate what you heard as a short numbered model, and ask one question at a time.
3. **Name what is deferred but not foreclosed.** For each deferred piece, say what the first cut must leave room for. For example, "the accountable-to field points at any actor, with a rule today that it must be a human."
4. **Stop when the settled part is small and clear.** Restate it in four or five lines, then confirm what is out of scope.
5. **Hand a tight scope to a build thread.** The brief carries the settled model, the deferred list, and the explicit out-of-scope list. The build thread opens a small PR ([recipe 24](../review-by-separate-thread/recipe.md)).

## Why it works

The expensive mistakes in agent work are built before the requirement settles ([recipe 18](../cost-reports/recipe.md) found one costing 8% of churn). A conversation is cheap. A tight scope also makes the PR small enough to review well.

## Pitfalls

- **Don't re-open deferred questions** in a new guise ([recipe 20](../stored-agenda/recipe.md)).
- **Watch for scope the director didn't ask for.** Our director's example mentioned "commenter" and "editor" roles. Those turned out to be a permission model change, not part of the identity change, so they were left out. When in doubt, ask whether an aside is in scope.
- **The coordinator may not see the code.** A lean that "fits the current schema" is a guess until a thread checks it.

## Example

> Settled for [A]:
> [1] Actors keep a stable identity and display name.
> [2] Each actor has immutable versions. A change to the delegation chain creates a new one.
> [3] Every action is stamped with the actor version.
> [4] Deferred but not foreclosed: nesting, and a hook for outside definition changes.
>
> Out of scope: permissions and the document model.
