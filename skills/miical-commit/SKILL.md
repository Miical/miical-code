---
name: miical-commit
description: Prepare and create a local Git commit. Use when the user asks to commit current changes, organize a coherent local commit, or validate a proposed commit message; require final confirmation before staging or committing, and do not push.
---

Create a commit only when the user explicitly asks for one. Do not push,
rebase, squash, or amend unless the user separately requests that operation.
If the target repository defines an explicit commit format or commit workflow,
follow it in preference to this default workflow.

## Gather Context

Inspect the repository state and both staged and unstaged changes:

```bash
git status --short
git diff
git diff --cached
```

Check recent commit titles when useful.

## Define the Commit Scope

Identify one coherent change to commit. Preserve unrelated user changes and
pre-existing staged content. If staged content cannot be safely separated
from the requested change, stop and explain the conflict instead of modifying
the user's staging area without permission.

## Validate the Change

Run checks relevant to the proposed change. Do not claim a check passed unless
it was actually run. Keep the staging area unchanged while preparing the
commit preview.

## Compose the Message

When the target repository does not define its own format, follow Conventional
Commits 1.0.0:

```text
<type>(<scope>)!: <description>

[optional body]

[optional footer(s)]
```

- Start with a required type. The `(<scope>)` and `!` shown in the template are
  optional; when present, place them before the required `: ` separator.
- Use `feat` for a new feature and `fix` for a bug fix. Other types are allowed;
  common choices are `build`, `chore`, `ci`, `docs`, `style`, `refactor`, `perf`,
  `test`, and `revert`.
- Put the required short description immediately after `: `.
- Separate the optional free-form body from the description with one blank line.
- Separate optional footers from the body with one blank line. Write each footer
  as a Git-style trailer such as `Refs: #123` or `Reviewed-by: Name`.
- Mark a breaking change with `!` immediately before `:`, or with an uppercase
  `BREAKING CHANGE: <description>` footer.

Write a concise title. Add a body when the reason for the change, an important
tradeoff, or migration guidance would not be clear from the title and diff
alone. Never bypass repository hooks with `--no-verify`.

## Request Final Confirmation

Before staging or committing, show the user:

- The proposed title and body, if any.
- The explicit list of files to include.
- Checks run and their results.
- Any unrelated or pre-existing staged changes that will remain untouched.
- A statement that the commit will remain local and will not be pushed.

Wait for explicit confirmation such as "confirm", "commit", or "go ahead".
The initial request to prepare a commit starts this workflow but does not
replace final confirmation of the preview. Do not run `git add` or `git commit`
before that confirmation.

If any candidate file changes after the preview, refresh the diff and request
confirmation again.

## Commit and Report

After confirmation, stage only the approved files with
`git add -- <path>...`. Do not use `git add .` or `git add -A`, because they
can capture unrelated work.

Inspect the final staged diff and check it for whitespace errors:

```bash
git diff --cached --check
git diff --cached
```

Create the local commit, then report its hash, title, checks run, and remaining
worktree state. Do not push the commit.
