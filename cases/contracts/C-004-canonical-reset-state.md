# C-004 Canonical Reset State

Related judgments: J-010, J-011
Source samples: 016

## Context

Evaluation reset selection used task maps, reverse maps, seeds, async flags,
and helper layers with no single identity for a reset state.

## Before

The same state could be addressed through several combinations. Consumers
defensively handled alternative forms and ordering was difficult to reason about.

## Decision

Represent every state as `(task_id, trial_id, reset_state_id)`. Filter by task,
flatten once, and shard by global process identity while preserving environment
order. Remove seeds when the reset-state identifier already determines state.

## After

Selection, sharding, logging, and reset execution share one representation.
Reverse maps, unused async options, and defensive validations disappeared.

## Why

A canonical identity simplifies every downstream operation and exposes invalid
inputs immediately.

## Rejected alternatives

- Accept several tuple/dict representations at reset time.
- Retain a random seed in addition to a unique reset-state identifier.

## Boundary

A genuinely different simulator source may normalize its native identifier at
the environment boundary before entering this contract.

## Evidence

Evaluation sharding retained deterministic environment ordering with fewer maps
and branches.
