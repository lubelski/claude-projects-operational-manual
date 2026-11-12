# 24. Review by a separate thread

Origin: a second project (cloud threads only, no build machine), November 2026.

Related: [recipe 10](../merge-authority/recipe.md) decides who may merge what, by risk. [Recipe 12](../light-testing/recipe.md) relies on the worker's own attestation. This recipe is about how the coordinator gets a sound basis for its approval. It can stand alone, or supply the coordinator's approval inside recipe 10.

## Problem

The coordinator approves merges but may have no repo access. Its approval then rests only on the author's report. And when the repo has no CI (continuous integration), the author's local check is the only gate.

## Recipe

**Rule (project instructions):** threads open PRs for tracking, and may merge once the coordinator has reviewed and approved.

1. **The author thread opens a small PR** and runs the repo's local check (ours was `pnpm check`).
2. **The coordinator asks a different thread to review it.**
   - Design-level PRs go to the chief of staff ([recipe 04](../chief-of-staff/recipe.md)).
   - Routine PRs go to a one-off review thread.
3. **The reviewer checks out the head commit,** runs the checks, and posts findings as a PR comment with a verdict: approve, or required changes.
4. **For test changes, the reviewer breaks each behavior.** Change the source one behavior at a time, and confirm that exactly the matching new test fails. Run flaky-looking tests many times. In our case, 8 deliberate breaks each failed exactly one new test, and 20 runs all passed.
5. **The coordinator approves or sends back** based on the review. The author folds in fixes and merges.
6. **Keep PRs small.** Small PRs keep reviews fast and make the reviewer's breaks practical.

## Why it works

The reviewer has no stake in the author's choices, and reads the code itself. Breaking each behavior proves the tests test something, which "all tests pass" can't. The coordinator gets an evidence-based verdict without repo tools.

## Pitfalls

- **A same-account reviewer can't approve on GitHub.** Every thread acts as the same GitHub user as the author, so a formal approval is refused. Post the review as a comment. The record is the comment, not GitHub's review state.
- **No CI means the check is only as good as the people who run it.** Both author and reviewer should run it on the pushed commit. Consider adding CI; [recipe 12](../light-testing/recipe.md) argues for keeping it narrow.
- **A review thread per PR adds a step.** For tiny changes it may be more than they need. Recipe 10's risk split is one way to decide which PRs get one.
- **Optional nits are fine.** Our reviewer marked two small issues as non-blocking, so the merge didn't wait on them.

## Example

> Verdict: approve. The diff is tests only, 70 lines in one file. I broke each behavior in the source, one at a time, and each of the 8 breaks failed exactly the matching new test. The file passed 20 runs in a row. The local check passes on the head commit. Two optional nits, neither blocks merge.
