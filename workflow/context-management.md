# Context Management

## Contents

- [Locate the store](#locate-the-store)
- [Find the task](#find-the-task)
- [Report attachment](#report-attachment)
- [Root index](#root-index)
- [Task index](#task-index)
- [Pitfalls](#pitfalls)
- [Playbooks](#playbooks)
- [Scripts](#scripts)
- [Size limits](#size-limits)
- [Detached work](#detached-work)
- [Update discipline](#update-discipline)

Maintain task-scoped working memory under `.miical_code` at the context root.
Use this structure:

```text
.miical_code/
├── INDEX.md
└── <task-id>/
    ├── INDEX.md
    ├── pitfalls/
    │   ├── INDEX.md
    │   └── <problem>.md
    ├── playbooks/
    │   ├── INDEX.md
    │   └── <action>.md
    └── scripts/
        ├── INDEX.md
        └── <verified-script>
```

Every directory must contain an `INDEX.md` that explains its direct children.
Use lowercase kebab-case task IDs that describe the outcome. Add a date or
sequence only to resolve a collision.

## Locate the store

Resolve one context store before executing an attached task or Goal:

1. Use a location explicitly selected by the user for this task or Goal.
2. Otherwise resolve the current Git repository root with
   `git rev-parse --show-toplevel` and check `<repo>/.miical_code`.
3. If the repository store does not exist, check `~/.miical_code`.
4. If neither exists, ask the user to choose whether to create the store in the
   current repository, at `~/.miical_code`, or at a custom location.

Treat a directory as an existing context store only when its `INDEX.md` exists.
If a `.miical_code` directory exists without `INDEX.md`, report the incomplete
store and ask whether to initialize it; do not silently skip it for another
store. When no current Git repository exists, skip the repository check and
offer only the global or a custom location.

Select only one store. Do not merge repository and global task catalogs. Keep
the selected path fixed until the attached task or native Goal completes or
becomes blocked, even if later commands change working directory. Never search
above the Git root or scan unrelated filesystem locations for another
`.miical_code`.

## Find the task

Read the root index first. Search task names, purposes, and task indexes when
needed. A lexical or technical resemblance is not sufficient to reuse a task.

Treat a candidate as the same task only when all applicable facts agree:

- it pursues the same final outcome;
- it changes or investigates the same core artifacts or system boundary;
- the request continues, corrects, or completes the existing acceptance
  conditions.

Create a new task when the deliverable is distinct, even if it uses the same
technology or touches the same module. Do not reuse a completed task for new
scope; create a new task and link the prior task if its knowledge is useful.
Initialize the task index and all three child directories and indexes before
executing a newly created task.

## Report attachment

Resolve the store and task silently. Do not announce that repository, store,
or task discovery is about to happen.

After selecting or creating the attached task, print this receipt in the
conversation before beginning its work:

```text
Miical context attached
task: <task-id>
path: <absolute-task-directory>
```

Use the selected task directory, not the store root, for `path`. Print the
receipt once when the attachment is established. Do not repeat it during later
continuations unless the attached task or path changes. When work only consults
prior context and does not attach, print no attachment receipt.

If no context store exists and user selection is required, ask for that choice
directly. Do not precede the question with a progress message about searching
for a repository or context store.

## Root index

Keep `.miical_code/INDEX.md` as the fast task catalog:

```markdown
# Tasks

| Task | Scope | Purpose | Status | Updated |
|---|---|---|---|---|
| [fix-worker-timeout](fix-worker-timeout/) | `.` | Fix false worker timeouts | active | 2026-07-18 |
```

Use only `active`, `blocked`, or `complete` for status. Keep each purpose within
40 characters. Use `.` as scope for a repository-local store and the canonical
repository path for a global store. Do not put execution details in this file.

## Task index

Use `<task-id>/INDEX.md` as the first document read when resuming work:

```markdown
# <Task title>

## Objective

<Stable intended outcome.>

## Current State

<Current verified state, unresolved boundary, and relevant constraints.>

## Key Timeline

- YYYY-MM-DD HH:MM:SS UTC: <Key event and result.>

## Next Action

<One concrete action.>
```

The task index must not repeat its repository scope or list the fixed
`pitfalls/`, `playbooks/`, and `scripts/` directories. The selected context
store, root task catalog, and child indexes already own that information. Keep
the `Scope` column in the root index because a global store can catalog tasks
from multiple repositories.

Record only events that change understanding, direction, capability, or
completion state. Use second-precision UTC timestamps backed by logs, file
times, or another authoritative source. Never invent missing timestamp
precision; omit an event until its exact time can be established. Keep at most
20 timeline entries and each entry within 60 characters. When the limit is
reached, merge the oldest related entries into a single milestone summary.
Never keep a command-by-command log.

## Pitfalls

Store one confirmed problem per file under `pitfalls/`. Include only:

```markdown
# <Problem>

## Symptom
## Cause
## Resolution
## Prevention
```

Record confirmed causes and effective resolutions. Keep hypotheses in the task
index until evidence confirms them. List every file in `pitfalls/INDEX.md` with
a one-line description.

## Playbooks

Store one proven standard action flow per file under `playbooks/`. Include only:

```markdown
# <Action>

## Use When
## Preconditions
## Procedure
## Success
```

Promote a procedure to a playbook only after it succeeds at the real boundary.
List every file in `playbooks/INDEX.md` with a one-line description.

## Scripts

Store only scripts that have run successfully. A stored script must have clear
inputs, outputs, invocation, and no secrets or machine-private absolute paths.
Re-run a script after modifying it before treating it as verified.

List every script in `scripts/INDEX.md` with its purpose and exact invocation:

```markdown
# Scripts

| File | Purpose | Run |
|---|---|---|
| `check-worker.sh` | Verify worker heartbeat | `bash scripts/check-worker.sh` |
```

Do not store failed experiments, speculative snippets, or one-off commands as
verified scripts.

## Size limits

Measure the whole Markdown file with `wc -m` and `wc -l`. Keep both measures at
or below the limit:

| Document | Characters | Lines |
|---|---:|---:|
| `.miical_code/INDEX.md` | 2000 | 150 |
| `<task-id>/INDEX.md` | 1000 | 100 |
| Any child directory `INDEX.md` | 800 | 80 |

Keep every child description within 50 characters. Detailed pitfall and
playbook documents should stay focused on one subject; the hard limits above
apply specifically to directory indexes.

When an index exceeds a limit, compress it before continuing work:

1. Remove duplication and facts available directly from linked artifacts.
2. Rewrite prose as short factual statements.
3. Merge completed timeline entries into milestone summaries.
4. Move necessary detail into the directly owned child document.
5. Preserve task identity, current state, unresolved risks, proven knowledge,
   and the next action.

Do not solve overflow by silently dropping tasks or files from an index. If the
irreducible inventory itself cannot fit, split it by a clear category and make
the parent index describe each resulting child index within the same limits.

## Detached work

When yielding after starting a background process, distinguish these claims:

- launch succeeded;
- the process was running at the last check; and
- the process completed successfully.

Record the durable job identifier, exact launch time, last checked time and
state, verification performed, and one executable status or artifact check.
Never describe a job as currently running or healthy without a timestamped
check, and never use successful launch as evidence that its full workflow
completed.

Keep the task `active` when its objective requires the background outcome. A
launch-only objective may be `complete` after launch verification, but its
current state must still say that the background outcome is unverified. Do not
promote a detached procedure to a playbook until it succeeds at the claimed
boundary.

On continuation, inspect the authoritative process state and artifacts before
relying on the recorded status. Correct exited, failed, or otherwise stale
claims immediately.

## Update discipline

- Update context after a key milestone, confirmed finding, decision, or change
  to the next action.
- Update the root index when task status or update date changes.
- Prefer rewriting the current snapshot over appending history.
- Remove or correct stale claims immediately.
- Never store conversations, secrets, raw logs, or routine edit history.
- Read the smallest sufficient context: root index, selected task index, then
  only relevant child indexes and files.
