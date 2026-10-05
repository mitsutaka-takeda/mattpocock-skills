## What it does

`implement-spec` takes a [spec](https://www.aihero.dev/ai-coding-dictionary/spec) and its [tickets](https://www.aihero.dev/ai-coding-dictionary/ticket) and implements the whole task graph on one **integration branch**. It uses the current [agent](https://www.aihero.dev/ai-coding-dictionary/agent) by default, reviews the completed branch with [code-review](https://aihero.dev/skills-code-review), and resolves work through the configured tracker.

The **frontier** contains unfinished tickets whose blockers are already integrated. The agent recomputes it after each ticket, so dependency order drives the build. Parallel [subagents](https://www.aihero.dev/ai-coding-dictionary/subagent) are an optional mode you request explicitly; invoking the skill does not request them.

## When to reach for it

You invoke this by typing `/implement-spec`, and the agent won't reach for it on its own.

| Your situation | Reach for |
| --- | --- |
| A spec and dependency-ordered tickets that you want implemented in one run | `/implement-spec` |
| One ticket you want to drive yourself | [implement](https://aihero.dev/skills-implement) |
| A spec that has not been split into tickets | [to-tickets](https://aihero.dev/skills-to-tickets) |

## Prerequisites

Provide the spec and tickets, including their acceptance criteria and blocking edges. The tracker instructions determine how tickets are read and resolved. [setup-matt-pocock-skills](https://aihero.dev/skills-setup-matt-pocock-skills) can supply missing tracker configuration; implementation from already supplied requirements can continue while independent tracking questions are settled.

## The integration branch

The current agent builds each ready ticket with [tdd](https://aihero.dev/skills-tdd), records its completion and advances the frontier. Once every ticket is implemented, it reviews the whole integration branch, fixes in-scope findings and verifies the affected behaviour. A second broad review is justified by remaining risks or failures rather than repeated automatically.

| Tracker or request | Delivery |
| --- | --- |
| You request a PR, or the tracker closes work through PRs | Open a draft after a meaningful commit, then update its evidence and mark it ready after required checks pass |
| Local tracker with no PR requirement | Finish on the integration branch and resolve tickets as the tracker specifies |
| Explicitly requested parallel work | Independent tickets get owned files and separate worktrees; the current agent integrates and reviews the result |

In parallel mode, workers start from the integration branch, build with `tdd`, and integrate its latest tip before reporting completion. Shared files or uncertain ownership keep a ticket sequential. [Context pointers](https://www.aihero.dev/ai-coding-dictionary/context-pointer) carry the spec, tickets and source notes without copying the same exploration into every task.

## Common questions

**Does it need GitHub or a PR?**

No. The output is the integration branch. A PR is needed only when requested or required by the tracker, so a local markdown tracker can finish offline.

**Will it start subagents automatically?**

No. This fork uses the current agent by default. Request multi-agent work explicitly when independent tickets benefit from it; capacity and safe file ownership still determine what can run concurrently.

**Why are completed blockers still shown as open on GitHub?**

Issues closed by a PR stay open until the PR merges. The agent therefore computes the frontier from work already integrated into the branch, rather than treating the tracker's open count as the build's completion state.

**When does the review happen?**

After all tickets are implemented. Reviewing the entire spec earlier would mistake intentionally unbuilt tickets for defects. Fixes receive focused checks, with wider verification only when the repository requires it or an unresolved risk warrants it.

## It's working if

- Tickets start in dependency order and the frontier advances as work is integrated.
- Each behavioural ticket is built with a meaningful red-green check.
- Already settled decisions and useful source notes carry across tickets.
- The final review checks the completed branch against the whole spec.
- The run ends on one integration branch, with a PR only when requested or required.

## Where it fits

`implement-spec` is the whole-spec build step after [to-tickets](https://aihero.dev/skills-to-tickets), an alternative to driving [implement](https://aihero.dev/skills-implement) once per ticket. It closes out with [code-review](https://aihero.dev/skills-code-review); you can invoke [retro](https://aihero.dev/skills-retro) afterwards to improve the environment. [ask-matt](https://aihero.dev/skills-ask-matt) maps the surrounding flow.
