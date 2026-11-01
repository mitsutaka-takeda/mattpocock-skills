---
name: chief-of-staff
description: Pursue an agreed long-running objective and maintain shared, source-backed project memory.
disable-model-invocation: true
---

Advance the user's agreed long-running objective, carrying decisions and evidence across tasks. Work on two tracks: complete the immediate task, and identify changes to the environment that would improve later tasks. Make those changes within the authorized scope; record other candidates without delaying the requested work.

## Establish the scope

Read the project's instructions and existing objective, status and completion records. Reuse settled decisions and authorization. Establish what outcome the current request covers, what evidence will show completion, and which dependencies remain. Ask only for missing information that changes that outcome, continuing independent authorized work while a required answer is pending.

An invocation starts the requested work in this conversation. Create a durable goal or recurring automation only when the user requests one, using the available harness tools and their completion rules. Suggest a useful schedule when the goal warrants it; a suggestion alone does not create one.

## Execution

Use the current agent for research, implementation, review and follow-up by default. Delegate only when the user explicitly requests multi-agent work for this task; invoking this skill alone does not request it.

For authorized delegation, give each independent task a bounded scope, source pointers and completion criteria. Start every worker with a fresh context window rather than a fork of this conversation. Use background execution when supported so the conversation can continue, and isolate concurrent writing tasks in separate worktrees. Workers complete their assignments directly without further delegation. Reconcile their evidence and changes before counting the work complete.

Keep communication sparse and concrete: the changed state, supporting evidence and next decision. Reuse notes and source paths instead of repeating exploration. Finish the current requested scope, or identify the concrete dependency preventing further progress, and record the remaining work for continuation.

## Shared memory

Look first for the shared project records or wiki the user and other agents already maintain. Follow the project's canonical paths and conventions, including the separation between a shared vault and an external code repository. Update those records in place rather than creating a parallel wiki. If a new wiki is needed and no location is established, agree its location with the user before creating it.

For a wiki:

- `index.md` lists pages with a link and one-line summary, grouped by topic.
- Each page covers one decision, recurring problem, subsystem or preference and links related pages.
- Issues, PRs, transcripts and execution reports remain sources; cite them rather than copying or editing them.

Maintain it through three operations:

- **Ingest:** update every affected page and the index when evidence establishes a durable fact or decision.
- **Query:** consult the index and relevant pages before a decision; preserve a useful new conclusion with its evidence.
- **Lint:** inspect contradictions, orphan pages, broken references and claims superseded by newer evidence. A recurring lint schedule can be proposed when useful.

Write historical claims with dates. For code, cite the repository and commit at which the claim held. Mark a superseded claim and add the new dated evidence; distinguish that history from current project summaries maintained under the project's conventions.

## Supporting workflows

Before describing or using another skill, locate its installed `SKILL.md` and read it. Resolve skills by name through the harness or its skill directories; source-repository bucket paths may differ from the installed layout. Use the workflow when it is available and its invocation policy permits it; otherwise continue the requested work directly or identify the missing prerequisite.

- **Retrospective:** use `retro` when a completed chunk or failed attempt reveals an environmental problem. For explicitly delegated work, inspect sessions periodically, prioritizing failures. Select actionable improvements supported by that evidence and pursue those within the agreed scope.
- **Large build:** carry settled requirements through `to-spec`, `to-tickets` and `implement-spec` when that build is requested. Preserve one integration branch, task dependencies and the final review. Reuse an existing spec or tickets instead of generating replacements.

## Improve the environment

Consider whether a failure calls for a constrained interface, a type, an automated check, a documented standard or a better test seam. Prefer a shared correction over a one-off workaround. Verify proposed improvements against the actual failure and the relevant repository checks.

Use the data sources the task needs, such as logs, the relevant test environment or the browser, within the existing access and change permissions. Keep implementation, evidence and blockers distinct. Report success only for the requested outcomes the evidence supports, and preserve the next step when work remains.
