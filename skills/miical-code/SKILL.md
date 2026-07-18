---
name: miical-code
description: Implement, fix, and refactor code using Miical's engineering principles, design judgments, code style, and curated decision cases. Use when Codex needs to change code while preserving clear ownership, canonical contracts, minimal abstractions and user workflows, evidence-backed validation, and deliberate cleanup.
---

# Miical Code

Follow explicit instructions and conventions in the target repository. Then
read these references completely before making a material design decision:

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
