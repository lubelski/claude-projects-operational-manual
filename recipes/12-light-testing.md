# 12. Light testing: attest, revert first, measure

## Problem

Hosted CI for a desktop app is expensive, and a full test gauntlet on every PR turns the merge queue into an operational and cost problem. But merging on faith is worse. It's tempting to design a big tiered system up front: verifiers, nightlies, release gates.

## Recipe

Start light, and measure before adding process.

1. **Keep hosted CI narrow on purpose.** Run only cheap checks in hosted CI. Say so in the docs, so nobody reads "CI passed" as "the app was built".
2. **Workers attest.** Each worker builds and runs the test suite in its own worktree on the pushed commit. It reports the SHA, the build result, and the test counts in the PR. A later push voids the attestation.
3. **Check main at the start.** Before starting work, confirm main builds and passes. Report it if not.
4. **Revert first.** If a merge breaks main, revert it immediately, then fix forward on a branch. A revert needs no approval ([recipe 10](10-merge-authority.md)).
5. **Log every incident** on one tracker issue: a red main, a revert, or a bug that reached the installed app. That log is the measurement.
6. **Review the numbers on a date.** Adopt heavier tiers (an independent re-run on the build machine, a nightly suite, a release gate) only where the log shows a problem.

These four lines in `AGENTS.md` were enough for us:

```
- Build and run the tests on the pushed commit; put the SHA and results in the PR.
- Check main is green before you start; report it if not.
- If a merge breaks main, revert first.
- Log every broken main, revert, and installed-app bug on <TICKET>.
```

## Why it works

main isn't production. The installed app on the director's machine is. Fast merges with quick reverts cost less than a slow gate, as long as you can see the failures. The log tells you when that stops being true.

## Pitfalls

- **Over-design.** We wrote a full tiered design (attestation scripts, a watcher that reverts on red, a nightly known-good tag) before measuring anything. The director parked it as a reference. The light version shipped in four lines.
- **Merge skew.** Two green PRs can break main together. Reverting first covers it. A required up-to-date check is the heavier answer.
- **Hand-test areas.** Window, drag, and text-input changes can't be attested by tests alone. Mark them higher risk, and get a person to try a dev build ([recipe 13](13-pull-based-test-builds.md)).
