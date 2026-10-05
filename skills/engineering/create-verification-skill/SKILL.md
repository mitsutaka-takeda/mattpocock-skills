---
name: create-verification-skill
description: Create or adapt a project-local Codex skill for repeatable verification of real application behaviour. Use when asked to establish a reusable verification workflow.
---

# Create Verification Skill

Give a future agent a repo-specific way to exercise the application and retain evidence of the outcome. Deliver a usable verification skill and validate its instructions on a representative feature before calling it ready.

## Discover the verification surface

Use the requested project and feature scope. Inspect its existing run commands, harnesses, and relevant verification guidance; extend an existing skill when it already owns the workflow. Prefer the repository's supported tooling over introducing another harness.

Establish how a user reaches the behaviour, what observable result proves it, and what setup is needed. Identify instance ownership, fixture data, required access, and external side effects. Resolve facts from the repository or a local observation; ask only for missing access or product choices that materially affect the result. Preserve existing authorization and keep verification within the intended environment.

## Build the project skill

Use the user's destination, or `.agents/skills/verify-<project>/` within the target repository. Create `SKILL.md` with a short `name` and a `description` that identifies the application and verification task. Keep shared operating guidance in the entrypoint; link feature-specific detail only where a feature needs it.

Capture the operational contract using actual repository commands and handles:

- **Run and identify:** prerequisites, launch or build command, readiness signal, and a check that the instance is the intended build and belongs to this run. Reference maintained scripts instead of copying their internals.
- **Exercise and observe:** drive the public UI, CLI, API, or library interface with the existing harness. State the expected output and relevant side effects. Keep fixture setup distinct from the action being verified.
- **Evidence:** record the tested revision and local changes, relevant conditions, actions, assertions, and results in a named location. Preserve evidence after cleanup and keep secrets out of captured output.
- **Isolation and cleanup:** isolate writable state and ports where supported, and track resources created by this run. Release those resources on success or failure while retaining evidence and pre-existing user state. Document shared-instance constraints when isolation is unavailable.

Add a compact feature map for the requested scope, or a small representative set of core features when scope is unspecified. Each entry connects a user action to a runnable check and observable expected outcome. Mark coverage limits and unexecuted entries. Split feature details into linked files when that makes selective reading useful; a small map can remain inline.

Add helper scripts only when they make repeated execution more reliable. Document their invocation and make failed assertions produce a failing exit status. Keep model selection, delegation, and unrelated development policy outside the generated skill.

## Validate the deliverable

Follow the generated instructions through setup, a representative feature, evidence capture, and cleanup. Confirm that assertions check the intended behaviour and that the evidence survives teardown. Validate added helpers on the paths used by this run. Correct defects in the generated workflow and rerun affected checks until it works.

If an application defect or missing access blocks the run, identify the failing command and prerequisite, continue independent authoring, and label the result as a draft with an explicit validation gap. Application repairs beyond the user's scope are separate work. Avoid inventing credentials, selectors, or successful observations to complete the document.

Return the generated paths, how to invoke the skill, the feature actually exercised and its evidence, and remaining coverage or environment limits. A successful representative run validates the workflow for that feature, not the whole feature map.
