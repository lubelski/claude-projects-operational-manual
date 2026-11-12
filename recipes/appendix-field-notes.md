# Appendix: field notes

Short incident notes, with product details removed. Each links to the recipe it shaped.

## The coordinator who couldn't read the backlog

The coordinator had no repo or tracker tools. Its plans came from worker reports, and it missed that CI built nothing and that several tickets were stale. Fix: a chief-of-staff thread writing Library files. [Recipe 04](chief-of-staff/SKILL.md).

## "Merge if CI passes" with no CI

The project rule said agents merge when CI passes. The only workflow ran on script changes and checked Python syntax, so every PR "passed" with zero checks. Fix: we named the real gate (the worker's attested build and tests) and kept CI narrow on purpose. [Recipe 12](light-testing/SKILL.md).

## Five ways to not merge a PR

Merges from the build machine were refused by auto mode despite a repo allow rule, an `AGENTS.md` policy, the director's relayed "ship it", and a fresh session. A cloud thread could merge. The cause: auto mode reads its own rules only from user-level settings, and treats relayed approval as no approval. Fix: one unconditional `autoMode.allow` sentence, added by the director. [Recipe 11](auto-mode-merges/SKILL.md).

## Agents can't edit their own rules

Both a build-machine session and a cloud thread refused to commit an `AGENTS.md` change that granted merge authority ("Self-Modification"). They were right to refuse. Fix: an IT ticket with a paste-in prompt and a patch. [Recipe 17](it-tickets/SKILL.md).

## The misfiled workspace

The tracker connector was signed into a personal workspace. The first two tickets landed there, and after the reconnect they had to be re-filed and the old copies cancelled by hand. Fix: verify the connector's workspace from a fresh thread before filing. [Recipe 08](connectors/SKILL.md).

## The stray served folder

The first machine visible to the project was serving an unrelated folder, because Remote Control happened to be running there. Running `/remote-control` inside a session didn't register the right folder. `claude remote-control` from the repo did. [Recipe 06](remote-control/SKILL.md).

## Built before the requirement settled

A whole UI pane was built, then removed two days later when the product model changed. It was about 8% of all code churn in the period, the largest single cost the first report found. Lesson: for anything that changes the object model, settle the intent ticket first. [Recipes 16](tickets-express-intent/SKILL.md) and [18](cost-reports/SKILL.md).

## Over-designing the test strategy

Asked for a tiered confidence model, an agent produced a full system: attestation scripts, a watcher, nightlies, release tags. The director's response: measure before prescribing. Four lines of guidance shipped instead, with a log and a review date. [Recipe 12](light-testing/SKILL.md).

## Push became pull

Getting test builds to the director's laptop started as a push design over a private network. The director flipped it to a menu-bar app that pulls and builds any ref. There's less to maintain, and agents don't need access to the laptop. [Recipe 13](pull-based-test-builds/SKILL.md).

## Small win, honestly reported

A "make old sessions load faster" PR measured its own gain: about 10 ms out of 250 ms. It said so, and named the real cause (the external tool's startup). Honest numbers in a PR are worth more than the change. [Recipe 09](pull-requests/SKILL.md).
