---
name: implement-spec
description: "Implement a specification and its dependency-ordered tickets on one integration branch, using a single agent by default."
disable-model-invocation: true
---

Implement the supplied spec and its tickets on one **integration branch**, resolving each ticket the way the issue tracker closes work. The tickets form a **task graph**: the **frontier** contains incomplete tickets whose blockers are complete.

Use the current agent for research, implementation, integration, review and fixes. Delegate only when the user explicitly requests multi-agent work for this task; invoking this skill alone does not request delegation.

## Process

1. Read the spec, ticket dependencies and supplied tracker instructions, or `docs/agents/issue-tracker.md` when present. Reuse the decisions and authorization already given. If tracker configuration needed to read or resolve tickets is missing, tell the user to run `/setup-matt-pocock-skills`; continue independent authorized work from supplied requirements. Ask only about missing information that materially affects the result.
2. Research the relevant code and documentation as needed. Reuse concise notes and source paths across tickets instead of repeating exploration.
3. Create the integration branch. Open a draft PR only when the user requests one or the tracker closes work through PRs, after the branch has a meaningful commit; link the spec and tickets it will close. A local tracker can finish on the branch without pushing or opening a PR.
4. Implement one frontier ticket at a time on that branch. Call the Skill tool with `tdd` for each ticket's behaviour. Run relevant tests and required checks, record completion on the integration branch, then recompute the frontier from integrated work rather than waiting for tracker issues to close. If no ticket is ready while work remains, report the actual blocker rather than marking the spec complete.
5. Once every ticket is implemented, call the Skill tool with `code-review` on the integration branch in the current agent. Resolve substantiated in-scope findings and rerun affected checks after fixes. Complete repository-required checks, expanding verification only for uncovered risks or failures.
6. Reconcile the result with every acceptance criterion. If a draft PR exists, update its description and validation evidence and mark it ready when required checks pass. Otherwise resolve each ticket as the tracker requires and report the integration branch. Report remaining blockers honestly.

## Explicit multi-agent mode

When the user requests delegation, assign only independent frontier tickets to subagents, each with ownership of its files or module and a separate worktree and branch based on the current integration branch. Share the spec, ticket and relevant source paths. Tell each worker that others are working in the codebase, to preserve their changes, and to implement its assigned ticket directly without further delegation, calling the Skill tool with `tdd`. Before reporting done, each worker integrates the current integration-branch tip and reruns affected checks.

The current agent integrates completed branches, resolves conflicts using their intent, updates the frontier, and performs the final review and fixes. A task that cannot be isolated safely stays sequential. Follow the requested agent count and available capacity; use one agent if delegation is unavailable and disclose that limitation.

Clean up only task-created worktrees after their work is integrated and no uncommitted changes remain, subject to the user's deletion permissions.
