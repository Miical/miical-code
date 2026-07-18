# Design Judgments

This is the complete, compact catalog of Miical design judgments. Read it in
full, then open only the detail files and cases relevant to the current task.

## Boundaries and ownership

### J-001 Place behavior with its semantic owner

- Signal: A component performs work whose meaning or lifecycle is defined elsewhere.
- Prefer: Move the behavior to the layer that owns its semantics and inputs.
- Over: Classifying by the current caller or a broad label.
- Details: [boundaries.md](details/boundaries.md#j-001-place-behavior-with-its-semantic-owner)
- Cases: C-001, C-002

### J-002 Preserve one-way dependency direction

- Signal: A lower layer imports a workflow, entrypoint, or other coordinator.
- Prefer: Invert the call or extract a lower-level capability.
- Over: Convenience imports that create cycles or reverse ownership.
- Details: [boundaries.md](details/boundaries.md#j-002-preserve-one-way-dependency-direction)
- Cases: C-001, C-002

### J-003 Give lifecycle state one owner

- Signal: Several objects track the same path, progress, resource, or status.
- Prefer: One owner with explicit operations and derived views.
- Over: Synchronized copies, secondary initialization, and repeated guards.
- Details: [boundaries.md](details/boundaries.md#j-003-give-lifecycle-state-one-owner)
- Cases: C-003

### J-004 Keep domain behavior out of generic utilities

- Signal: A helper owns a domain format, backend choice, configuration, or lifecycle.
- Prefer: Put it in the corresponding domain package.
- Over: Growing `utils` into an unowned dependency hub.
- Details: [boundaries.md](details/boundaries.md#j-004-keep-domain-behavior-out-of-generic-utilities)
- Cases: C-002

## Data, state, and configuration contracts

### J-010 Trace values to their producer

- Signal: Shape, range, identity, or field meaning is uncertain.
- Prefer: Inspect the producer and establish the contract at the source.
- Over: Guessing at each consumer.
- Details: [contracts.md](details/contracts.md#j-010-trace-values-to-their-producer)
- Cases: C-004, C-005, C-006

### J-011 Use one canonical representation and parse path

- Signal: Code accepts several shapes, prefixes, keys, or fallback locations.
- Prefer: One representation and one access path per identified data source.
- Over: Defensive `if`, `getattr`, shape guessing, or permissive parsing.
- Details: [contracts.md](details/contracts.md#j-011-use-one-canonical-representation-and-parse-path)
- Cases: C-004, C-005

### J-012 Declare supported configuration explicitly

- Signal: Stable fields are injected at runtime or flattened into unrelated YAML.
- Prefer: Typed fields and independently meaningful nested config groups.
- Over: `++` as permanent API, duplicate aliases, and implicit defaults.
- Details: [contracts.md](details/contracts.md#j-012-declare-supported-configuration-explicitly)
- Cases: C-007

### J-013 Derive rather than duplicate state

- Signal: Two stored values can disagree but one is derivable from the other.
- Prefer: Store the minimum authoritative state and derive the rest.
- Over: Parallel epoch/step, path, enable/value, or aggregate state.
- Details: [contracts.md](details/contracts.md#j-013-derive-rather-than-duplicate-state)
- Cases: C-003, C-008

### J-014 Keep runtime data out of native artifact configuration

- Signal: Dataset paths, statistics, adapter settings, or machine paths enter upstream config.
- Prefer: Runtime config and sidecar artifacts owned by the integration boundary.
- Over: Using native model config as a transport channel.
- Details: [contracts.md](details/contracts.md#j-014-keep-runtime-data-out-of-native-artifact-configuration)
- Cases: C-006, C-009

## Abstraction and reuse

### J-020 Abstract only after real repetition

- Signal: An interface is proposed mainly for possible future implementations.
- Prefer: Wait for multiple concrete implementations and a stable common contract.
- Over: Speculative Protocol, backend, exporter, result, or plugin layers.
- Details: [abstraction.md](details/abstraction.md#j-020-abstract-only-after-real-repetition)
- Cases: C-010

### J-021 Use the smallest abstraction that owns the behavior

- Signal: Several layers or types exist for one direct operation.
- Prefer: A method, function, or small state object at the owning boundary.
- Over: Wrapper chains and one-implementation framework hierarchies.
- Details: [abstraction.md](details/abstraction.md#j-021-use-the-smallest-abstraction-that-owns-the-behavior)
- Cases: C-010, C-011

### J-022 Add compatibility only for an identified consumer

- Signal: Aliases, fallback prefixes, patches, or old paths are retained "just in case."
- Prefer: Name the consumer and test the path, or remove it.
- Over: Permanent compatibility for hypothetical users.
- Details: [abstraction.md](details/abstraction.md#j-022-add-compatibility-only-for-an-identified-consumer)
- Cases: C-012

### J-023 Reuse contracts, not names

- Signal: Components share a label but differ in inputs, state, or lifecycle.
- Prefer: Reuse only the stable semantic and mathematical core.
- Over: Forcing model-specific adapters or features behind a false common interface.
- Details: [abstraction.md](details/abstraction.md#j-023-reuse-contracts-not-names)
- Cases: C-013

### J-024 Preserve upstream-native implementations and formats

- Signal: Integration pressure suggests converting all models to one library or format.
- Prefer: Explicit builders and adapters around the upstream-native policy lifecycle.
- Over: Repackaging models only to satisfy a framework convention.
- Details: [abstraction.md](details/abstraction.md#j-024-preserve-upstream-native-implementations-and-formats)
- Cases: C-009, C-014

## User workflows and interfaces

### J-030 Expose one minimal entrypoint

- Signal: Users must understand internal scripts, Hydra composition, or setup stages.
- Prefer: One launcher named by user intent with only necessary choices exposed.
- Over: Layered launchers and environment-variable matrices.
- Details: [workflows.md](details/workflows.md#j-030-expose-one-minimal-entrypoint)
- Cases: C-015

### J-031 Maintain one supported workflow

- Signal: Docker, native, legacy, or model-specific paths duplicate the same outcome.
- Prefer: One authoritative, continuously verified path.
- Over: Multiple uncertain paths connected by disclaimers.
- Details: [workflows.md](details/workflows.md#j-031-maintain-one-supported-workflow)
- Cases: C-015, C-016

### J-032 Derive related outputs from one run root

- Signal: Users repeat paths for metrics, video, logs, checkpoints, or cache.
- Prefer: One run/output root with deterministic subpaths.
- Over: Several independently configurable paths that can disagree.
- Details: [workflows.md](details/workflows.md#j-032-derive-related-outputs-from-one-run-root)
- Cases: C-016

### J-033 Keep orchestration out of examples and entrypoints

- Signal: User-facing scripts construct models, clusters, datasets, or algorithms.
- Prefer: Thin entrypoints into reusable workflows.
- Over: A second framework implementation in examples.
- Details: [workflows.md](details/workflows.md#j-033-keep-orchestration-out-of-examples-and-entrypoints)
- Cases: C-001, C-017

## Evidence, reliability, and performance

### J-040 Prove the real execution closure

- Signal: Completion is inferred from imports, static checks, or image builds.
- Prefer: Execute the smallest real training, evaluation, rendering, or recovery path.
- Over: Substituting a weaker gate for the requested outcome.
- Details: [validation.md](details/validation.md#j-040-prove-the-real-execution-closure)
- Cases: C-018, C-019

### J-041 Diagnose from stage-specific evidence

- Signal: A distributed, runtime, or performance failure is described only as "stuck" or "slow."
- Prefer: Identify the failing stage and inspect its authoritative state.
- Over: Simultaneous speculative changes across layers.
- Details: [validation.md](details/validation.md#j-041-diagnose-from-stage-specific-evidence)
- Cases: C-020, C-021

### J-042 Match the claim to the validation scope

- Signal: Narrow checks are used to support broad compatibility or runtime claims.
- Prefer: State exactly what was and was not proven.
- Over: Treating absence of a static error as end-to-end success.
- Details: [validation.md](details/validation.md#j-042-match-the-claim-to-the-validation-scope)
- Cases: C-018

### J-043 Test only durable, meaningful behavior

- Signal: Tests target private helpers, forwarding, defaults, or hypothetical branches.
- Prefer: Algorithms, statistics, state transitions, scheduling, and artifact round trips.
- Over: Coverage that freezes incidental implementation.
- Details: [validation.md](details/validation.md#j-043-test-only-durable-meaningful-behavior)
- Cases: C-022

### J-044 Measure before optimizing

- Signal: A performance change is proposed without knowing the dominant cost.
- Prefer: A minimal attributable measurement, then optimize the largest relevant budget.
- Over: Rewriting the easiest component or degrading quality without evidence.
- Details: [validation.md](details/validation.md#j-044-measure-before-optimizing)
- Cases: C-021, C-023

## Change scope and evolution

### J-050 Remove obsolete paths and residue

- Signal: A migration or experiment leaves old files, flags, aliases, or debug state.
- Prefer: Delete the whole obsolete path after consumers move.
- Over: Default-off remnants and permanent dual paths.
- Details: [evolution.md](details/evolution.md#j-050-remove-obsolete-paths-and-residue)
- Cases: C-012, C-024

### J-051 Update all consumers in one migration

- Signal: A responsibility, name, config path, or module moves.
- Prefer: Update imports, targets, scripts, docs, and tests together.
- Over: Compatibility shims that hide an incomplete migration.
- Details: [evolution.md](details/evolution.md#j-051-update-all-consumers-in-one-migration)
- Cases: C-001, C-024

### J-052 Keep a change coherent and authorized

- Signal: A refactor creates opportunities for unrelated cleanup or behavior changes.
- Prefer: One coherent scope with explicit assumptions and proportionate validation.
- Over: Bundling opportunistic changes into the same task.
- Details: [evolution.md](details/evolution.md#j-052-keep-a-change-coherent-and-authorized)
- Cases: C-025

### J-053 Preserve unrelated user work

- Signal: The worktree contains changes outside the requested task.
- Prefer: Inspect, isolate, and leave them untouched.
- Over: Broad staging, cleanup, or rewriting for convenience.
- Details: [evolution.md](details/evolution.md#j-053-preserve-unrelated-user-work)
- Cases: C-026

### J-054 Make handoffs executable

- Signal: Work crosses machines, agents, or long interruptions.
- Prefer: Record verified state, blockers, commands, success criteria, and next action.
- Over: Narrative summaries or reliance on chat memory.
- Details: [evolution.md](details/evolution.md#j-054-make-handoffs-executable)
- Cases: C-027

## Naming and explanation

### J-060 Name by responsibility and user intent

- Signal: Names expose implementation history or duplicate their parent context.
- Prefer: Domain roles for internals and user goals for public entrypoints.
- Over: Generic `runner`, repeated `_env`, or implementation-specific commands.
- Details: [readability.md](details/readability.md#j-060-name-by-responsibility-and-user-intent)
- Cases: C-001, C-015

### J-061 Explain decisions, not syntax

- Signal: Comments and docs restate fields or code while omitting constraints and reasons.
- Prefer: Explain ownership, units, tradeoffs, exceptions, and verified usage.
- Over: Line-by-line narration and duplicated defaults.
- Details: [readability.md](details/readability.md#j-061-explain-decisions-not-syntax)
- Cases: C-028
