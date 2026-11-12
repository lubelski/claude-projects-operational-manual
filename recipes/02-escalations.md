# 02. Escalations the director can answer from the chat

## Problem

"PR #123 needs a yes from you" forces the director to open the PR, read the diff, and work out the risk. That's the manager's job. An escalation without context is just a transfer of work.

## Recipe

Every escalation to the director carries four things, then the options:

1. **What the change does**, in one or two sentences, in user terms.
2. **The evidence**: the test results, a screenshot or render, and timing numbers. Say what was not verified.
3. **The risk**: low or higher, and why. Name the parts that only a human can test.
4. **Why it needs the director**: a policy rule, a safety check that wants a human, a product call, or a step agents may not take.

Then give lettered options, recommendation first, each with its consequence.

Put it in the project instructions so every future coordinator does it:

```
Every escalation to me says what the change does, the evidence, the risk,
and why it needs me, so I can decide from the chat.
```

## Why it works

The director can decide from the message alone. Writing the four parts also makes the coordinator check its own reasoning. Sometimes, while writing "why it needs you", it finds the answer is "it doesn't".

## Pitfalls

- **Batch the asks.** If three things wait on the director, send one message with numbered items, not three pings.
- **Don't repeat a decision card in prose.** Ask once.
- **Report honest gaps.** "The window behavior can only be tested by hand, and nobody has done it yet" is worth more than "all tests pass".

## Example

> **Escalation: PR #124, input box auto-height**
> - **What it does:** the input starts one line tall and grows to 10 lines, then scrolls. The scrollbar sits at the right edge.
> - **Evidence:** the build passes and all 190 tests pass. Renders at 0, 4 and 20 lines are in the PR.
> - **Risk:** low to medium. Typing has not been tested by hand, and the scrollbar position can't be seen in renders.
> - **Why it needs you:** the build machine's safety check refused the merge on my approval alone.
>
> Options:
> a) Merge now, and you check typing in the installed app.
> b) You try a dev build first.
