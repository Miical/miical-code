# C-010 Export on the Owning Base Class

Related judgments: J-020, J-021
Source samples: 043, 096

## Context

A proposed `PolicyExporter` Protocol and `SavePretrainedPolicyExporter` would
mediate native export for every TrainableModel.

## Before

Only the TrainableModel knew how to separate its policy state and required
artifacts, so the exporter layer mostly forwarded arguments.

## Decision

Define native export behavior directly on the TrainableModel base contract and
override it only when a real integration requires different behavior.

## After

One ownership boundary replaces an exporter hierarchy, while integrations can
still implement their native lifecycle.

## Why

The model wrapper already owns the policy and artifact knowledge. A separate
one-implementation abstraction adds indirection without enabling substitution.

## Rejected alternatives

- Keep the Protocol for future models.
- Define backend classes for every upstream library before multiple implementations exist.

## Boundary

If export later becomes an independently configured service with several
interchangeable implementations, a separate abstraction may become justified.

## Evidence

Removing the exporter layer left all current integrations expressible through
their owning model contract.
