# C-017 Shared Evaluation Workflow

Related judgments: J-001, J-033
Source samples: 009, 046, 079

## Context

RECAP needed policy evaluation and users also needed a standalone eval CLI.

## Before

Evaluation risked becoming a RECAP-specific stage copied into a separate CLI
for other models.

## Decision

First establish evaluation as a reusable Cluster/workflow capability. Make
`vvla-eval` a thin entrypoint and let the RECAP policy-eval stage call the same
workflow. Keep model and simulator differences behind their adapters/contracts.

## After

Standalone, RECAP, Pi0, and Arena evaluation share lifecycle, metrics, videos,
and environment semantics.

## Why

Evaluation orchestration is independent of the first algorithm that needs it.

## Rejected alternatives

- Copy the RECAP stage into an eval entrypoint.
- Branch the workflow by concrete model name.
- Let examples construct workers and resource pools directly.

## Boundary

A model integration still implements its own policy I/O and capability; sharing
the workflow does not force identical model internals.

## Evidence

RECAP callers migrated to the common path and complete benchmark evaluation
produced the same metrics structure as standalone execution.
