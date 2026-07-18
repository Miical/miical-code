# C-005 Image Range Follows the Producer Contract

Related judgments: J-010, J-011
Source samples: 058

## Context

Pi0.5 SFT loss decreased unusually slowly. The adapter divided every image by
255.

## Before

LeRobot dataset images were already normalized floats, while simulator images
arrived as uint8 values. Treating both as 0..255 divided dataset images twice.

## Decision

Trace both supported producers. Normalize uint8 simulator images once and pass
already normalized dataset floats unchanged. Reject unknown numerical contracts
rather than adding broad range guessing.

## After

Dataset training and simulator rollout both deliver the numerical range expected
by the native policy.

## Why

The word `image` does not define dtype or range. The producer contract does.

## Rejected alternatives

- Always divide by 255 for consistency.
- Infer arbitrary formats from min/max at every call.
- Fix the symptom by changing learning rate or training duration first.

## Boundary

An explicit new data source may add one named normalization branch at its
adapter boundary.

## Evidence

Inspection of real dataset and simulator outputs identified the duplicate
scaling before the adapter was changed.
