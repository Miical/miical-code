---
name: miical-goal
description: Pursue a user-defined objective through Codex's native Goal lifecycle while preserving explicit task context in .miical_code and applying Miical engineering standards to code changes. Use when the user asks Codex to start, continue, or persistently complete a substantial multi-step goal across context windows or automatic continuations.
---

# Miical Goal

Use Codex's native Goal mechanism for persistence, continuation, budgets, and
terminal status. Do not build a second task loop or status system.

Read [`../../workflow/context-management.md`](../../workflow/context-management.md)
completely before starting or continuing goal work.

## Enter the goal

1. Inspect the native Goal state. Use its unfinished objective when one exists;
   otherwise use the objective explicitly supplied with this invocation.
2. Silently resolve the context store in this order: an explicit user-selected
   location, `.miical_code` in the current Git repository root, then
   `~/.miical_code`. Do not announce this discovery step.
3. When neither default store exists, ask the user to choose the repository,
   global, or a custom location. Do not create a store before that choice.
4. Ensure the selected store has `KNOWLEDGE.md` as defined by the context
   protocol, then read it before the root task index.
5. Inspect the selected `.miical_code/INDEX.md` before executing the goal.
6. Treat similar tasks only as candidates. Resume an existing task only when
   its intended outcome, core work objects, and acceptance boundary identify
   the same task.
7. Otherwise create a new task directory and register it in the root index.
8. Print the attachment receipt defined by the context protocol.
9. Read the selected task's `INDEX.md`. Read child indexes and linked files only
   when they are relevant to the next action. Follow explicit references to a
   prior task when they concern the boundary you will act on.
10. Reconcile recorded context with the user's latest instruction and current
   workspace state. Correct stale context before relying on it.
11. When no native Goal exists, create one from the explicit objective after
   selecting its task context. Never replace an unfinished native Goal.

The user's latest instruction and the actual workspace are authoritative.
`.miical_code` is external working memory, not a second source of truth for Goal
status.

Keep the selected context store fixed until the native Goal reaches a terminal
state. Changing the process working directory must not change the store.

## Execute

- Preserve the user's objective. Change the plan when evidence warrants it,
  but do not silently narrow the outcome.
- Use the native Goal lifecycle to continue until the objective is actually
  complete or its strict blocked condition is met.
- When creating, changing, fixing, or refactoring code, load and follow
  `$miical-code`. Do not duplicate its engineering rules here.
- Record only durable context: key milestones, confirmed findings, resolved
  pitfalls, proven procedures, and scripts that have actually run successfully.
- Run the context protocol's complete context closure after each key milestone
  and before yielding a continuation. Updating the task index alone is
  insufficient when evidence qualifies for a pitfall, playbook, script, or
  proven-knowledge entry. Keep `Next Action` singular and executable.
- When prior knowledge materially changes the goal and succeeds at its claimed
  boundary, update `KNOWLEDGE.md` once for that item across the task's
  continuations.
- When yielding after launching detached work, apply the context protocol's
  detached-work rules. On continuation, refresh the process state before
  relying on the recorded status.
- Validate every completion condition with current evidence before completing
  the native Goal. Mark the task complete in `.miical_code/INDEX.md` only when
  the native objective is complete.

Do not stage or commit `.miical_code` unless the user explicitly requests it or
the target repository defines it as a tracked project artifact.
