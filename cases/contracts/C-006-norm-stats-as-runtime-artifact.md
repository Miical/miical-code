# C-006 Normalization Statistics as a Runtime Artifact

Related judgments: J-010, J-014
Source samples: 037, 045

## Context

Pi0 state and action normalization statistics were embedded in native model
configuration and tied a base model to one dataset.

## Before

Using mismatched statistics produced losses near `1e11`. Runtime paths and
dataset facts risked leaking into exported `config.json`.

## Decision

Compute or recover statistics from the authoritative training source, store
them as `norm_stats.json`, and pass the path through the integration runtime.
Normalize only real dimensions before policy padding. Export the sidecar with
the policy but keep runtime paths and fields out of native config.

## After

Training loss returned to a normal range, exported artifacts were self-contained,
and the upstream model configuration remained native.

## Why

Statistics describe the policy/data relationship, not the policy architecture.

## Rejected alternatives

- Hard-code statistics in the base model.
- Recompute statistics from a convenient but historically incorrect dataset.
- Use a ContextVar or engine special case to hide the path transport.

## Boundary

If an upstream format officially defines normalization as part of its native
processor artifact, preserve that official artifact rather than inventing a sidecar.

## Evidence

The full 52,970-frame dataset produced 8 state and 7 action dimensions; a real
30-step training run produced loss around 0.04-0.20.
