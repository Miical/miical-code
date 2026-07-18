# C-026 Preserve Unrelated Work

Related judgments: J-053
Source samples: 029, 102

## Context

Commit and issue workflows were used in worktrees with pre-existing staged,
unstaged, and untracked changes.

## Before

Broad staging or cleanup could capture or overwrite work outside the requested
change.

## Decision

Inspect the complete status and diffs, identify one coherent candidate set,
leave unrelated changes untouched, request final confirmation, and stage only
explicit approved paths. Never use broad staging for convenience.

## After

Local commits include the approved change while unrelated RECAP/DAgger or other
user files remain unchanged and visible.

## Why

The shared worktree is user state, not disposable agent workspace.

## Rejected alternatives

- `git add .` after visually reviewing only part of the diff.
- Reset or format unrelated files to obtain a clean status.
- Treat the initial commit request as approval of an unseen scope.

## Boundary

If candidate and unrelated work are inseparable in the same hunks, stop and
explain the conflict instead of modifying staging silently.

## Evidence

Commit previews named exact files and post-commit reports listed the untouched
worktree changes.
