---
name: retro
description: "Conduct a retrospective on a coding session."
disable-model-invocation: true
---

The user has asked for a **retrospective**. You are suggesting improvements to the coding agent's **environment** to improve future runs. Ground each finding in session evidence or an observed gap in the repository's checks. Implement improvements when the user has requested implementation; otherwise finish with actionable recommendations.

## Steps

1. Call the Skill tool with `writing-for-agents` for the writing style guide.

2. Read the primary sources for the session the user specifies. This may mean searching through session logs on this machine. If the user doesn't specify a session, default to the current one.

3. Look for candidates for improvement in these categories.

- **Navigation**: how easy was it for the agent to find the right files? Are there hidden dependencies between files? Would a **navigation pointer** make it easier? _Use when_ the session took a long time to find a piece of information.
- **Automated checks**: inspect the repo's lint/check scripts, hooks and CI before proposing a check. An existing check that is unwired or broken is a finding to repair. Flag the absence of both a pre-commit hook and a CI job running lint, typecheck or tests as a **guardrail** gap. _Use when_ an automated check could have caught a session mistake, or no guardrail exists.
- **Coding standards**: classify a missed violation before proposing a rule. **Mechanical** violations (fixed syntax, banned APIs, import shapes, file locations) belong in deterministic checks; prefer the smallest effective addition to the repo's existing linter, hooks or CI. Reserve `CODING_STANDARDS.md` for **judgement calls**, such as contextual design consistency. _Use when_ review missed a mistake or an existing standard needs clarification or removal.
- **Global AGENTS.md**: are there any steering instructions that should be moved to coding standards (or automated checks) instead? _Use when_ the AGENTS.md file is particularly large - in the repo OR the user's global scope.
- **Tool economy**: did the agent make expensive tool calls that could be streamlined? Is there any custom tooling (CLI's, MCP's) that is particularly token-inefficient? _Use when_ the agent made an expensive tool call.
- **No-ops**: look for instructions in steering files that don't modify the agent's behavior. _Use when_ the steering files are large and unwieldy.
- **Information access**: look for opportunities to increase the agent's access to information. Teeing dev server logs, readonly access to third-party services. _Use when_ a crucial piece of information was not available to the agent.

4. Present candidates in severity order, with the evidence, the proposed improvement and how to verify it. Distinguish implemented and verified changes from recommendations and unverified assumptions.

## Reference

### Implementation vs Review

Implementation and review are phases the current agent can perform. Delegate only when the user explicitly requests it. Implementation needs applicable standards while changing code; review checks the result against those standards and the requirements, reading surrounding code when the diff alone is insufficient. Put mechanically enforceable rules in automated checks so both phases benefit.

### Files

You have access to several files in the repo:

- `CLAUDE.md`/`AGENTS.md`: these files are pushed to the context window of any agent working in this repo. They should be used incredibly sparingly, usually only for **navigation pointers** to other files.
- `CODING_STANDARDS.md`: keep judgement-based standards here for implementation and review. Move branch-specific detail into referenced docs when it obscures the rules needed for the current task, with **navigation pointers** stating when to read it.
- Docs: use docs as references files, pointed to by other files. Look for existing docs before writing new ones.
- Skills: use skills for docs (since their description goes into the agent's context window), or for user-invoked commands. Follow the advice in the `writing-for-agents` skill.
