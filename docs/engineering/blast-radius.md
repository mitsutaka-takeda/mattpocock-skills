## What it does

Assess what a change could break beyond its edited lines. The assessment tests the safety assumptions on which the change depends and makes any untested assumptions visible.

## When to reach for it

In Codex, type `$blast-radius`, or let it activate when the task calls for downstream impact analysis.

- Use it when a small-looking change affects consumers, persisted data, or execution ordering.
- Use [code-review](https://aihero.dev/skills-code-review) for a broader review against standards and requirements.
- Use [diagnosing-bugs](https://aihero.dev/skills-diagnosing-bugs) when the starting point is a reported failure to diagnose.

## Safety assumptions

A useful result explains what must remain true and what evidence supports it. For a cache change, that could be whether active entries survive eviction. A focused check against the actual implementation can resolve that question; the report states which conditions it exercised.

An assessment can finish with unresolved assumptions when execution is unavailable. Those gaps remain visible alongside the evidence needed to resolve them.

## It's working if

- Each material finding explains a reachable failure and points to relevant code.
- You can rerun the decisive check from the reported command and conditions.
- You can distinguish observed results from assumptions still awaiting verification.

## Where it fits

A standalone impact assessment that complements [code-review](https://aihero.dev/skills-code-review). Use [ask-matt](https://aihero.dev/skills-ask-matt) to find neighbouring workflows.
