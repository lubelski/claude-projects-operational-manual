# Claude Projects operational manual

These are recipes for shipping software with a Claude project: a coordinator, a set of worker threads, one or more machines, a tracker, and a human who directs. They come from running a real project, a desktop app built by agents on a dedicated build machine. Product details are left out on purpose.

These are field notes, not a specification. Each recipe records what we did, why we did it, and what bit us. The platform changes quickly. Treat any claim about tool behavior as dated, and check it against current docs before you rely on it.

## Who this is for

A person who runs a Claude project and wants agents to ship real changes while they stay out of the weeds. It assumes you know what a pull request, a worktree, and an issue tracker are.

## Vocabulary

| Term | Meaning here |
|---|---|
| **Director** | The human. Sets goals, makes product and policy calls, approves risky changes. |
| **Coordinator** | The project's own Claude session. It talks to the director in the project chat, starts threads, and acts as the engineering manager. |
| **Thread** / **worker** / **IC** | A Claude session started for one piece of work. It may run in a cloud container or on a machine through Remote Control. |
| **Chief of staff** | A long-lived thread whose job is to read the code and the tracker for the coordinator. See [recipe 04](recipes/04-chief-of-staff.md). |
| **Library** | The project's shared file folder. Every thread and the coordinator can read it. |
| **Standing orders** | Rules that agents follow because they read them, not because a system enforces them. See [recipe 03](recipes/03-where-standing-orders-live.md). |
| **Build machine** | A machine that agents drive on their own. See [recipe 05](recipes/05-two-machine-modes.md). |
| **Personal machine** | The director's own machine. Agents act on it only when asked. |

## Recipes

**A. Operating model**
1. [Director, manager, and ICs](recipes/01-director-manager-ics.md)
2. [Escalations the director can answer from the chat](recipes/02-escalations.md)
3. [Where standing orders live](recipes/03-where-standing-orders-live.md)
4. [A chief-of-staff thread](recipes/04-chief-of-staff.md)

**B. Machines**

5. [Two machine modes](recipes/05-two-machine-modes.md)
6. [Connecting a machine with Remote Control](recipes/06-remote-control.md)
7. [Worktree hygiene](recipes/07-worktree-hygiene.md)
8. [Account connectors versus machine-local config](recipes/08-connectors.md)

**C. Shipping**

9. [The pull request is the artifact](recipes/09-pull-requests.md)
10. [Merge authority as standing orders](recipes/10-merge-authority.md)
11. [Auto mode and merges](recipes/11-auto-mode-merges.md)
12. [Light testing: attest, revert first, measure](recipes/12-light-testing.md)
13. [Pull-based test builds](recipes/13-pull-based-test-builds.md)
14. [Stacked PRs and merge order](recipes/14-stacked-prs.md)

**D. Tracking**

15. [One shared tracker login](recipes/15-shared-tracker-login.md)
16. [Tickets express intent](recipes/16-tickets-express-intent.md)
17. [IT tickets for the human](recipes/17-it-tickets.md)
18. [Routine cost reports](recipes/18-cost-reports.md)

**Appendix:** [Field notes](recipes/appendix-field-notes.md)

## Recipe format

Each recipe has the same five parts:

- **Problem:** what goes wrong without it.
- **Recipe:** the steps or the rule.
- **Why it works:** the reasoning, so you can adapt it.
- **Pitfalls:** what bit us.
- **Example:** a short sample, with names changed.

## Contributing

Add a recipe when a procedure has worked at least once and you would do it again. Date any claim about how a tool behaves. Keep product names, machine names, and private paths out.
