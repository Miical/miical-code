# C-019 Real Pi0.5 Training Closure

Related judgments: J-040
Source samples: 035

## Context

A new Pi0.5 Dockerfile needed to work from a clean CUDA image through real SFT.

## Before

Metadata and imports looked plausible, but native build tools, LIBERO assets,
noninteractive configuration, optional model imports, tokenizer behavior, and
runtime limits had not been exercised together.

## Decision

Continue through each real boundary until the native checkpoint loaded, FSDP
initialized, a real LeRobot batch arrived, backward/optimizer steps completed,
and loss metrics were emitted. Fix the owning boundary exposed by each failure
rather than adding unrelated dependencies.

## After

The image passed real LIBERO CPU rendering and completed 72 Pi0.5 SFT optimizer
steps on the same dataset used for the comparison workflow.

## Why

An image that builds is not a training environment until the intended training
operation executes.

## Rejected alternatives

- Stop after package installation or model import.
- Install OpenVLA dependencies into Pi0 to hide central registration coupling.
- Disable tokenizer despite the policy requiring task text.

## Boundary

A smoke run proves the execution closure, not convergence or full-scale training quality.

## Evidence

The run loaded the 3B checkpoint, used approximately 37 GB GPU memory, and
emitted real loss/gradient metrics for 72 steps.
