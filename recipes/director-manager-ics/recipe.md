# 01. Director, manager, and ICs

## Problem

A Claude project starts many threads quickly. If the director talks to each thread directly, they become the router. They have to remember which thread owns what, read every report, and repeat context. The project then moves only as fast as the director reads.

## Recipe

Give everyone a role from an ordinary engineering org, and write the roles into the project instructions.

- **The director (the human)** stays in the project chat by default. They set goals, make product and policy calls, and approve risky changes. They can step into a thread, but they shouldn't need to.
- **The coordinator** acts as the engineering manager. It splits requests into threads, tracks who is blocked on what, reviews worker output, gates merges, and turns worker questions into decisions the director can answer in one line.
- **Threads** act as ICs (individual contributors). Each owns one piece of work from start to merge. They report to the coordinator, not to the director.

Then add these working rules:

1. When the coordinator relays a thread's question, it brings enough context that the director can decide without opening the thread ([recipe 02](../escalations/recipe.md)).
2. Decisions use lettered or numbered lists, so the director can reply "1B, 2A". A second project extended this to every list in chat, with stable tags ([recipe 19](../referencable-labels/recipe.md)).
5. The coordinator summarizes thread results in the chat. It links the thread for detail, but the summary stands alone, so the director goes into a thread only when something is out of the ordinary.
3. The coordinator passes the director's answer back to the thread by attaching the director's own message, not by paraphrasing it. A relayed paraphrase is not the director's approval.
4. Several threads may run at once. Don't optimize the org chart before it hurts. Revisit roles at retrospectives ([recipe 23](../output-triggered-retrospectives/recipe.md)).

Here is a sample project-instructions snippet:

```
## Working model
- I am the director. The coordinator is the engineering manager. Threads are ICs.
- I stay in the project chat. Bring thread questions and decisions here, with
  context and lettered options, so I can reply with picks.
- Pass my answers back to threads by attaching my message.
- Avoid sending me into threads.
```

### Variant: roles held loosely

From a second project. Instead of writing the model as rules, state the analogy and say it is gestural. That project's description said, in effect: "The coordinator acts like an engineering manager, threads like ICs, and the user like a director. This is gestural more than literal, and meant to evolve." Rules then accrete from real friction. Each time the director states a preference ("label your lists", "keep the chief of staff high level"), the coordinator saves it to memory, and promotes it to standing orders when it becomes a rule ([recipe 03](../where-standing-orders-live/recipe.md)).

This suits the start of a project, when the director doesn't yet know which rules they want. The written snippet above suits a project whose rules have settled. The cost of the loose version: preferences in memory are recalled, not always read, so promote anything that keeps being missed.

## Why it works

It reuses a structure people already understand. The director's attention is the scarce resource, so the design spends it only on decisions. Stafford Beer's Viable System Model (VSM) is a useful lens. Threads are System 1 (operations), the coordinator is Systems 2 and 3 (coordination and control), and a chief of staff is System 3* (audit, [recipe 04](../chief-of-staff/recipe.md)). The director holds Systems 4 and 5 (direction and identity).

## Pitfalls

- **A coordinator with no tools is a router, not a manager.** In our setup the coordinator could not read the repo or the tracker. Everything it knew came from worker reports. Its plans were grounded secondhand and missed drift on the board. The fix was [recipe 04](../chief-of-staff/recipe.md).
- **"Approved" means different things to different readers.** A safety check on a machine may accept only the human's own words. See [recipe 11](../auto-mode-merges/recipe.md).
- **The director still gets pulled in.** When a worker needs something only a human can do, such as a permission change, the coordinator should file it as a ticket ([recipe 17](../it-tickets/recipe.md)) rather than send the director into the thread.

## Example

> **Director:** What's blocked on me right now?
>
> **Coordinator:** Waiting on you:
> 1. Commit the settings file (ticket ENG-xxx). This unblocks four PRs.
> 2. Pick for build delivery: A, B or C.
> 3. Next work batch: a) input height, b) drag-and-drop import, c) status markers. Pick any, or "all".
>
> In progress, nothing needed from you: the cost report thread.
