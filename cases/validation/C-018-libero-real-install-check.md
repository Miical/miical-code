# C-018 Real LIBERO Install Check

Related judgments: J-040, J-042
Source samples: 034

## Context

The Docker environment needed to guarantee that LIBERO worked without a GPU
during image construction.

## Before

Import and version checks could pass without OSMesa, BDDL/init-state resources,
scene assets, or working camera rendering.

## Decision

Before importing MuJoCo/LIBERO, select OSMesa. Check versions and assets, create
a `libero_spatial` environment, set a real initial state, execute an action, and
verify both camera images. Reserve GPU/EGL validation for container runtime.

## After

Docker build proves CPU headless simulation behavior rather than package presence.

## Why

The user depends on reset, step, and images; those operations define the minimum
meaningful installation closure.

## Rejected alternatives

- `python -c 'import libero'` as the image gate.
- GPU rendering during `docker build` where no GPU is available.
- Claim host success when the host has the wrong LIBERO version.

## Boundary

This check does not prove GPU training or EGL runtime and must not be reported
as doing so.

## Evidence

The final build created the environment, stepped it, and produced two valid
64-by-64 RGB images through OSMesa.
