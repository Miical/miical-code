# C-009 Native Policy and Training Wrapper

Related judgments: J-014, J-024
Source samples: 039, 042, 044

## Context

Pi0 arrived in Giga's native Diffusers format, while verl-vla needed SFT,
rollout, critic state, FSDP checkpoints, and Hugging Face publication.

## Before

The native model had been wrapped again as a Transformers AutoModel, mixing
policy configuration, runtime statistics, auxiliary state, and export logic.

## Decision

Keep one upstream-native policy inside a TrainableModel wrapper. Save the full
wrapper, optimizer, and auxiliary state in the training checkpoint. Export only
the native policy and required artifacts in the Hugging Face directory.

## After

Pi0 remains Diffusers-native, GR00T remains Transformers-native, and both use a
common training capability boundary without a common file format.

## Why

Training resumption and model publication are different products with different
state requirements.

## Rejected alternatives

- Convert every model to Transformers AutoClass.
- Put critic and runtime paths into native policy config.
- Publish the complete verl-vla wrapper as the upstream policy.

## Boundary

An upstream policy may itself include official processors or normalization
artifacts; those remain part of its native export.

## Evidence

An unmodified native Pi0 base trained, exported, and reloaded through the
upstream implementation without verl-vla-only config fields.
