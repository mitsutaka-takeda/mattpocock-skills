## What it does

Create a reusable Codex skill for verifying a project's real application behaviour. The generated instructions are exercised on a representative feature before the result is called ready.

## When to reach for it

In Codex, type `$create-verification-skill`, or let it activate when you request a reusable project verification workflow.

- Use it to establish or adapt a maintained verification entrypoint for a project.
- Use the project's existing verification skill when you only need to check a feature once.

## Prerequisites

A writable project checkout and enough tooling and access to exercise a representative feature. The default destination is `.agents/skills/verify-<project>/`. Missing runtime access leaves a clearly marked draft until the instructions can be validated.

## A reusable proof

The generated skill connects a user action to an expected result, with enough environment information to repeat it. It uses existing project tooling and retains evidence after temporary resources are cleaned up.

A feature map records the covered behaviours and their entrypoints. A representative successful run establishes that one path works; unexecuted features remain identified as such.

## It's working if

- A later session can locate the right application instance and run the documented check.
- Failed expectations are visible as failures.
- Evidence remains available after cleanup, and existing user state is preserved.
- The delivery report names the feature actually exercised and any remaining gaps.

## Where it fits

A project setup workflow that can be revisited as verification needs change. Its output supplies runnable evidence for [code-review](https://aihero.dev/skills-code-review) and [diagnosing-bugs](https://aihero.dev/skills-diagnosing-bugs). Use [ask-matt](https://aihero.dev/skills-ask-matt) to find neighbouring workflows.
