# C-024 Remove Experiment and Migration Residue

Related judgments: J-050, J-051
Source samples: 018, 050, 077, 086, 093

## Context

Absolute teleop control, image pruning, WebRTC, old Hydra overrides, aliases,
and compatibility code remained after their decisions had changed.

## Before

Disabled options still required states, docs, branches, imports, and tests. New
and old paths coexisted after consumers had moved.

## Decision

When an experiment fails or a migration completes, delete implementation,
flags, state, documentation, tests, empty packages, and compatibility aliases.
Search every consumer before removal and update the coherent set together.

## After

Only the selected path remains, with one configuration and execution contract.

## Why

Default-off code still increases the number of states the system can enter.

## Rejected alternatives

- Keep old behavior for possible future comparison.
- Leave aliases indefinitely after all in-repository consumers migrate.
- Preserve failed optimization code behind a feature flag.

## Boundary

Retain a migration path only for an identified external consumer and a defined
retirement condition.

## Evidence

Absolute-control state, WebRTC dependencies, old override paths, and unused
aliases were removed after searches confirmed their consumer status.
