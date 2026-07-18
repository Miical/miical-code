# C-001 Layered Execution Ownership

Related judgments: J-001, J-002, J-033, J-051, J-060
Source samples: 001, 003, 030, 031, 038

## Context

The repository had `main_*` entrypoints, Hydra composition, stage orchestration,
algorithm loops, and distributed execution mixed under trainer code.

## Before

Moving a file changed its location without clarifying whether it was a CLI,
workflow stage, trainer operation, or cluster lifecycle action. RECAP
`compute_return` and its loop configuration remained under `trainer` although
all consumers were workflows.

## Decision

Use a one-way execution model: entrypoints select configuration and call a
workflow; workflows orchestrate stages and lifecycle; trainers advance an
algorithm; TrainCluster owns topology and distributed operations; workers
execute inside processes. Move code and every import/Hydra target together.

## After

RECAP stages and configuration live under workflows. Trainers no longer import
workflows. EntryPoints remain thin and TrainCluster is a first-class domain.

## Why

The owner is determined by the decision being made, not by the first caller or
the broad fact that the code contributes to training.

## Rejected alternatives

- Add a generic `runner` directory without a precise responsibility.
- Move only `main_*` files and leave YAML and consumers behind.
- Keep workflow stages under trainer because they manipulate training data.

## Boundary

A trainer may call public Cluster operations and a workflow may call a trainer;
this does not transfer ownership of their internal decisions.

## Evidence

Imports, Hydra targets, stage callers, and workflow tests were updated together;
the obsolete `trainer/recap` package was removed.
