# Miical Code

Miical Code packages Miical's engineering judgment, workflows, and real
decision cases as reusable Codex Skills. This repository is the source of truth
for those capabilities; once installed, they can be invoked from any working
directory.

## Installation

Clone the repository and link each Skill into Codex's global Skills directory:

```bash
git clone https://github.com/Miical/miical-code.git
cd miical-code
mkdir -p ~/.codex/skills
for skill_dir in "$PWD"/skills/*; do
  ln -s "$skill_dir" ~/.codex/skills/"$(basename "$skill_dir")"
done
```

The links continue to point at this repository, so Skill changes take effect
without copying files. Run the link loop again after pulling an update that
adds new Skills.

## Usage

Invoke a Skill by entering its name and a task in a Codex conversation:

```text
$miical-code Refactor this module
$miical-commit
$miical-goal Complete this migration and continue until it is verified
$miical-help
```

| Skill | Purpose |
|---|---|
| `$miical-code` | Implement, fix, and refactor code using Miical's engineering judgment |
| `$miical-commit` | Review changes and create a local commit after final confirmation |
| `$miical-goal` | Use Codex Goal to pursue long-running objectives |
| `$miical-help` | List the currently available Miical Skills |

## Context

`miical-code` and `miical-goal` use `.miical_code` for reusable task context:

- Read the current repository's `.miical_code` first, then fall back to
  `~/.miical_code`.
- Reuse pitfalls, proven playbooks, and verified scripts from relevant tasks.
- Attach complex work to a task directory that tracks current state, key
  milestones, and the next action.
- Treat historical context as evidence, and correct stale or inaccurate
  guidance when current evidence contradicts it.

The context structure and compression limits are defined in
[`workflow/context-management.md`](workflow/context-management.md).

## Repository Structure

```text
skills/     Codex Skill entrypoints
profile/    Engineering principles, design judgments, and code style
cases/      Decision cases distilled from real changes
workflow/   Workflow protocols shared by multiple Skills
```

`miical-code` loads only the core judgments by default, then selects relevant
details and cases for the task to avoid consuming unnecessary context.
