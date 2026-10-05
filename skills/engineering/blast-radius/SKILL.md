---
name: blast-radius
description: Assess downstream breakage from a proposed change or diff, and verify the assumptions its safety depends on. Use for change-impact analysis beyond the edited code.
---

# Blast Radius

Determine what a change could break outside its edited lines. Deliver a supported impact assessment with runnable evidence for the decisive safety assumptions. Keep fixes outside an assessment-only request; local disposable probes are part of the investigation.

## Scope and contracts

Use the change and comparison established by the user. Record the relevant commits or working-tree state, including in-scope untracked files. For a proposal without code, assess the stated design and label conclusions that require an implementation.

Follow changed behaviour to the contracts its consumers rely on. Investigate the boundaries implicated by this change: persisted or wire data, indirect consumers, lifecycle ordering, shared state, configuration, or dependencies at their pinned versions and local patches. A caller list is a starting point; the result should explain a reachable failure or why that path remains valid.

## Decisive assumptions

Identify the facts that would make the change safe, and try to falsify them. For example, an eviction change may depend on active entries being retained; test that property through the cache implementation actually used by the application.

Choose the smallest observation that resolves each material uncertainty. Reuse applicable evidence from the same code and conditions; add a focused probe where it leaves a gap. Exercise the real implementation with an observable expected result. Use the running application when the claim depends on integration or timing that a smaller probe cannot establish.

Record the command, tested revision or working-tree state, conditions, expected result, and observed result. Distinguish an assertion failure from a setup failure. Preserve useful evidence outside disposable probe state. Source inspection can support a conclusion, but identify assumptions that remain untested and the reach of any passing probe.

If execution is unavailable, continue the supported analysis and identify the specific missing evidence. An untested safety assumption remains unresolved. Broaden the investigation only when a discovered dependency, failure, or unanswered material risk warrants it.

## Completion

Return the change's observable effect, the safety assumptions and their evidence, confirmed breakage, and unresolved risks. Give each finding a concrete failure path and source location; summarize cleared concerns only where they help the decision. State what was assessed and what was not, including the cheapest next check for a material gap.

Finish when the material impact paths are accounted for and each decisive assumption is supported, disproven, or explicitly unresolved. A clean assessment is valid; a passing probe establishes only the conditions it exercised.
