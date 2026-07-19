---
name: miical-code
description: Implement, fix, and refactor code using Miical's engineering principles, design judgments, code style, and curated decision cases. Use when Codex needs to change code while preserving clear ownership, canonical contracts, minimal abstractions and user workflows, evidence-backed validation, and deliberate cleanup.
---

# Miical Code

Follow explicit instructions and conventions in the target repository.

## Reuse task context

Before implementing, check for useful prior task context:

1. Resolve the current Git repository root and check its
   `.miical_code/INDEX.md`. If it does not exist, check
   `~/.miical_code/INDEX.md`.
2. Ensure the selected store has `KNOWLEDGE.md` as defined by the context
   protocol, then read it before the root task index.
3. Search task names, scopes, purposes, and task indexes for work with a similar
   outcome, system boundary, failure mode, or workflow.
4. Read the candidate task index first. Read only the relevant pitfalls,
   playbooks, and verified scripts linked from its child indexes. Follow every
   explicit cross-task reference that concerns the boundary you will act on;
   the reference is routing, not a substitute for its evidence.
5. Use prior tasks as evidence and precedent, not authority. Verify their
   assumptions against the user's current request and the actual repository.

Perform this lookup silently. Do not announce that repository or context
discovery is starting. When the work does not attach to a task, print no
attachment receipt.

Do not create a context store or task merely to handle a small, self-contained
change. If no existing context is useful, continue normally.

When current evidence shows that referenced context is wrong or stale, correct
the owning document and its index. Preserve historical facts, but replace false
current claims, invalid resolutions, and obsolete procedures. Remove a script
from the verified index when it no longer runs; add it back only after a
successful execution. Keep every correction within the context size limits.

After prior knowledge materially changes the work and succeeds at its claimed
boundary, update `KNOWLEDGE.md` using the protocol's counting and ranking rules.
Do not increment an item merely because it was read or attempted.

## Attach complex work

Attach the work to a `.miical_code` task when durable context would materially
improve execution, especially when it:

- is likely to require repeated user interaction or multiple continuations;
- has several dependent implementation, migration, or validation stages;
- contains evolving decisions, investigations, or unresolved risks; or
- produces reusable pitfalls, playbooks, or verified scripts.

Read [`../../workflow/context-management.md`](../../workflow/context-management.md)
completely before attaching. Reuse the task already selected by `$miical-goal`
when one exists. Otherwise resolve the context store using that protocol,
attach to the same task when a true match exists, or initialize a new task.
Print the attachment receipt required by that protocol, then update the task's
current state, key timeline, and next action after material milestones and
before yielding. Run the protocol's complete context-closure procedure; a task
index update alone does not replace qualifying pitfall, playbook, script, or
proven-knowledge updates. Mark it complete only after validating the actual
outcome.

Attaching context does not create a native Goal. Use `$miical-goal` when the
user asks for persistent autonomous execution.

## Apply the engineering profile

Read these references completely before making a material design decision:

- [`../../profile/principles.md`](../../profile/principles.md)
- [`../../profile/judgments.md`](../../profile/judgments.md)
- [`../../profile/code-style.md`](../../profile/code-style.md)

Use `judgments.md` as the complete decision catalog. Select only the detail
files relevant to the task:

- Ownership, layering, lifecycle, or `utils`: [`boundaries.md`](../../profile/details/boundaries.md)
- Tensor, `DataProto`, state, artifact, or Hydra contracts: [`contracts.md`](../../profile/details/contracts.md)
- Reuse, compatibility, wrappers, interfaces, or model formats: [`abstraction.md`](../../profile/details/abstraction.md)
- CLI, examples, documentation, outputs, or launchers: [`workflows.md`](../../profile/details/workflows.md)
- Testing, debugging, runtime proof, or performance: [`validation.md`](../../profile/details/validation.md)
- Refactoring, migration, cleanup, worktree safety, or handoff: [`evolution.md`](../../profile/details/evolution.md)
- Naming, comments, or explanation: [`readability.md`](../../profile/details/readability.md)

Read the relevant detail file completely. Usually one or two files are enough.

Open [`../../cases/INDEX.md`](../../cases/INDEX.md) and read one to three linked
cases only when:

- a judgment materially changes the implementation;
- several valid designs remain after applying the judgment;
- a judgment's boundary or exception is unclear;
- the proposed design resembles a historically rejected design; or
- the user asks for the reasoning or precedent.

Treat cases as evidence that explains judgments, not as additional rules. An
explicit current judgment wins over a historical case. Do not load files from
[`../../sample/`](../../sample/) during normal use; they are uncurated source
material for evolving the profile.

Before implementing, identify the relevant judgment IDs and resolve these
questions where applicable:

1. What component is the source of truth?
2. Who owns the meaning and lifecycle of the behavior?
3. What is the one supported data, configuration, or execution path?
4. Is each abstraction supported by real repetition and a stable contract?
5. What is the smallest complete user-facing workflow?
6. What evidence proves the requested outcome at its real boundary?
7. What old path or residue should disappear when the change is complete?
8. Which durable behavior, if any, warrants a dedicated test?

Use Codex's normal implementation workflow. Continue to follow applicable
instructions and constraints in the target repository. Do not mention profile
files or judgment IDs in code or user-facing output unless doing so helps the
user review a design decision.
