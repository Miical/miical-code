# C-003 Single Checkpoint State Owner

Related judgments: J-003, J-013
Source samples: 004, 013

## Context

Checkpoint paths, retention, resume state, current path, epoch, and dataloader
progress were distributed across Trainer and Cluster.

## Before

Several values described the same state. Additional initialization methods and
guards allowed partially initialized checkpoint behavior. Epoch inference was
ambiguous at exact boundaries.

## Decision

Create the checkpoint helper when its configuration is accepted. Let it own
path, retention, and resume operations. Let Trainer decide save timing. Persist
the dataloader/step state that determines continuation and derive epoch or
current path views.

## After

Checkpoint behavior has one owner, and resume continues from authoritative
data progress without guessing a parallel epoch state.

## Why

Duplicated mutable state eventually disagrees. Derived information should not
become a second source of truth.

## Rejected alternatives

- Maintain `current_checkpoint_path` beside a derivable path.
- Store both epoch and exact dataloader progress as independent authorities.
- Require callers to invoke a second `init_checkpoint()` method.

## Boundary

Trainer still owns the algorithmic decision of when a checkpoint is needed.

## Evidence

Resume handling covered exact epoch boundaries without special epoch guessing.
