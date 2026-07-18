# Change Scope and Evolution

## J-050 Remove obsolete paths and residue

A completed rollback or migration removes implementation, flags, aliases,
debug state, tests, documentation, and empty packages associated with the old
path. Default-off code is still maintained code.

## J-051 Update all consumers in one migration

When moving a responsibility or configuration path, search for Python imports,
Hydra targets, launchers, documentation, tests, checkpoints, and external
entrypoints. Update the coherent consumer set together. Avoid shims whose only
purpose is to make a partial migration appear complete.

## J-052 Keep a change coherent and authorized

Separate architectural migration from behavior changes unless both are needed
for the requested outcome. Preserve known working baselines and validate the
changed boundary. Do not expand the task because nearby code could also be
cleaned.

## J-053 Preserve unrelated user work

Inspect staged and unstaged changes before editing or committing. Work around
unrelated changes and stage explicit paths. Do not reset, broadly format, or
clean a worktree for convenience.

## J-054 Make handoffs executable

Record the objective, authoritative current state, completed evidence, exact
blocker, environment requirements, next command, success criterion, and
remaining work. Exclude speculative narration and details that do not change
the next action.
