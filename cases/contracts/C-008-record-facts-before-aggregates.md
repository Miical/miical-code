# C-008 Record Facts Before Aggregates

Related judgments: J-013
Source samples: 011, 015

## Context

Evaluation and RECAP data paths needed per-task metrics, global metrics, and
multi-iteration dataset accumulation.

## Before

Execution code maintained complex incremental aggregate state, while field
normalization and dataset merging were combined in helpers.

## Decision

Record primitive trajectory facts—length, success, task ID, and return—then
derive summaries. Keep field normalization, newly collected episode accumulation,
and merging with the SFT dataset as separate transformations.

## After

Raw evidence remains available, aggregate calculations are reproducible, and
each data transformation changes one semantic dimension.

## Why

Primitive facts are hard to reconstruct; aggregates and merged views are
derivable.

## Rejected alternatives

- Maintain per-task and global counters during rollout.
- Let `ensure_fields` also merge datasets.
- Use NaN for a field whose defined missing value is zero.

## Boundary

Streaming systems with bounded storage may aggregate online, but should still
define the primitive event contract first.

## Evidence

The resulting metrics could be regenerated from trajectory records and multi-round
datasets accumulated without overwriting prior episodes.
