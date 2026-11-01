---
name: implement
description: "Implement a piece of work based on a spec or set of tickets."
disable-model-invocation: true
---

Implement the work described in the supplied spec, tickets, or agreed conversation. Reuse settled decisions and existing authorization; ask only about missing information that materially changes the result, continuing independent work meanwhile.

If the user passes a ticket reference, fetch it from the issue tracker and state its title before starting. If the reference is ambiguous, ask while continuing independent authorized work.

Call the Skill tool with "tdd" where possible, at pre-agreed seams.

Run tests and typechecks relevant to the changed behaviour and complete repository-required checks. Use the full suite when required or when the affected scope warrants it. After checks pass, repeat or broaden them only for new changes, failures, or unresolved risks. Low-impact documentation or formatting edits need appropriate validation, not new tests that merely repeat the implementation.

Once done, call the Skill tool with "code-review" to review the work in the current agent unless the user explicitly requests delegation. Ensure the review includes the actual changes; the default committed diff excludes uncommitted work. Resolve substantiated in-scope findings before finishing.

Commit your work to the current branch.
