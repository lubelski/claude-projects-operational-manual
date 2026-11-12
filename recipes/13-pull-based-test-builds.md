# 13. Pull-based test builds

## Problem

The director wants to try main, a branch, or a PR on their personal machine. The first idea was **push**: the build machine copies builds over a private network, and a receiver installs them. That means giving agents a way into the personal machine, keeping a receiver running, and handling the case where the app is open. Or the director runs a Remote Control session on their own machine just to test, which puts agents on the personal machine again.

## Recipe

Flip it to **pull**: a small test-manager app on the personal machine.

1. A menu-bar app on the personal machine polls the repo for main, branches, and open PRs.
2. One or two clicks build (or download) and install the chosen ref.
   - **main** installs as the regular app.
   - **Branches and PRs** install as a separate dev app, with its own identifier and settings, so both run side by side ([recipe 05](05-two-machine-modes.md)).
3. It never replaces a running copy. It installs once the app quits.
4. It also has a CLI with JSON output (for example `install pr/125`), so an agent can drive it when asked.
5. Start by building from source on the personal machine. It's simpler, and the test manager itself will rarely change.

The coordinator's handoff for a hand test then becomes: "PR #125 is ready to try. Install `pr/125` from the test manager and check X and Y."

## Why it works

The personal machine stays under the director's control. No agent needs standing access to it, and testing no longer needs a Remote Control session there. The director pulls exactly what they want to try, when they want it.

## Pitfalls

- **A dev build may read its branch and commit from its source folder**, which won't exist on another machine. Stamp the commit in at build time.
- **Keep Remote Control on the personal machine for real exceptions only**, such as capturing a hang that only happens there. Turn it on for that job and off again.
- **Push designs aren't wrong.** Pull is simply less to maintain when one person tests.
