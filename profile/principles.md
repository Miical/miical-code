# Engineering Principles

These principles are the smallest stable description of Miical's engineering
judgment. Read all of them before making a material design decision. Use the
linked judgments for operational guidance and cases for evidence.

## P-001 Find the source of truth

Trace data, configuration, state, and behavior to the component that defines
their meaning. Do not make consumers guess what producers should have emitted.

Judgments: J-010, J-011, J-013

## P-002 Put responsibility with its semantic owner

Place a behavior where its meaning, lifecycle, and required information are
owned. Current call sites and broad labels such as "training-related" are not
ownership arguments.

Judgments: J-001, J-002, J-003, J-004

## P-003 Keep one canonical path

Prefer one configuration path, data representation, state owner, and user
workflow. Add alternatives only for distinct, identified sources or consumers.

Judgments: J-011, J-012, J-031, J-050

## P-004 Abstract from real repetition

Create an abstraction only after multiple real implementations reveal a stable
contract. Reuse shared semantics, not merely similar names.

Judgments: J-020, J-021, J-023

## P-005 Preserve upstream-native boundaries

Integrate upstream models, tools, and runtimes through explicit adapters while
preserving their native formats and lifecycle whenever possible.

Judgments: J-014, J-024

## P-006 Expose the smallest complete workflow

Minimize user decisions, not correctness. Provide one supported entrypoint,
derive internal settings from authoritative inputs, and fail clearly when a
real prerequisite is missing.

Judgments: J-030, J-031, J-032, J-033

## P-007 Require evidence at the claimed boundary

Completion must be proven at the level being claimed. Imports prove imports;
real training, evaluation, export, or recovery claims require those behaviors.

Judgments: J-040, J-041, J-042, J-044

## P-008 Remove obsolete complexity completely

When an experiment, migration path, alias, fallback, or compatibility layer no
longer has a concrete consumer, remove it and its residue.

Judgments: J-022, J-050, J-051

## P-009 Test durable behavior selectively

Spend test complexity on important algorithms, data transformations, state
transitions, and artifact round trips. Do not freeze trivial implementation
details or hypothetical branches.

Judgments: J-043
