# C-011 Small Early-Stopping State

Related judgments: J-021
Source samples: 012

## Context

SFT needed early stopping based on a fitted validation trend over one window.

## Before

The design introduced a result dataclass, repeated save-on-stop semantics, and
validation across several layers.

## Decision

Use one small state object: update it with metrics, return a normal metric dict,
and expose the stop decision as a property. Validate its config once.

## After

The mechanism remains subordinate to the training loop and does not create a
new result or checkpoint architecture.

## Why

One window and one boolean decision do not justify a hierarchy of policy and
result types.

## Rejected alternatives

- A dedicated result dataclass for every update.
- Duplicate `save_on_stop` behavior in both helper and trainer.
- Complex synchronization to prevent one prefetched step after stop.

## Boundary

A multi-objective stopping controller with independent consumers may deserve a
richer result model.

## Evidence

The simpler object preserved the intended trend decision and accepted the
explicit, understandable one-step async-prefetch behavior.
