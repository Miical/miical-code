# C-015 Minimal Supported Launcher

Related judgments: J-030, J-031, J-060
Source samples: 053, 054, 059, 067

## Context

The Pi0.5 SFT example accumulated nested scripts, environment variables,
preflight checks, explicit downloads, cache internals, and separate Docker and
native instructions.

## Before

Users had to understand implementation details before starting training. Some
automatic checks attempted to compute normalization statistics before the
dataset existed and produced misleading failures.

## Decision

Maintain Docker as the authoritative environment, name public commands
`run_train` and `run_eval`, expose only necessary choices, use standard model
and dataset loading, and document real preparation requirements directly.

## After

One launcher enters each supported workflow. Internal Hydra composition and
cache layout remain implementation details, while output and TensorBoard access
are predictable.

## Why

The user should choose the task, not reconstruct the framework's assembly.

## Rejected alternatives

- Maintain a second native workflow with a disclaimer.
- Expose every training override as an environment variable.
- Add defensive file and image checks for states the standard loader already handles.

## Boundary

A reusable library API may expose more parameters than a maintained example;
the example still selects one coherent, verified profile.

## Evidence

The final guide and launchers were repeatedly run from repository-local `.data`
and simplified after each unnecessary decision was identified.
