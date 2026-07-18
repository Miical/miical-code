# C-013 Critic Reuse at the Stable Boundary

Related judgments: J-023
Source samples: 041, 078

## Context

Pi0 and GR00T integrations both needed critics, target critics, and common
attention or MLP components.

## Before

The shared name suggested one generic critic abstraction, but policy features,
action encodings, task conditioning, and adapter configuration differed.

## Decision

Reuse stable mathematical building blocks and lifecycle patterns. Let each
model integration own feature extraction, action semantics, configuration, and
whether critic modules exist. Do not create placeholder modules when disabled.

## After

Common code reflects an actual contract while model-specific semantics remain
local and explicit.

## Why

Similarity of names does not guarantee substitutable inputs or ownership.

## Rejected alternatives

- One universal critic accepting loosely typed feature dictionaries.
- A top-level `auxiliary` dumping ground detached from the model adapter.
- Disabled critic placeholder modules for structural uniformity.

## Boundary

If several integrations converge on the same feature and action protocol, that
protocol can be promoted after it is demonstrated.

## Evidence

The comparison explicitly enumerated feature, action, target-update, and
checkpoint differences before choosing the shared layer.
