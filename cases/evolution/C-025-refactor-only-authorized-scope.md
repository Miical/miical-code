# C-025 Refactor Only the Authorized Scope

Related judgments: J-052
Source samples: 081

## Context

A repository-wide directory and configuration refactor touched paths used by a
Docker workflow known to work before the change.

## Before

It was tempting to adjust algorithm defaults, dependencies, and neighboring
cleanup while moving files.

## Decision

Treat the known runtime as a baseline and validate only what the refactor
changes: imports, package paths, Hydra targets, callers, and static composition.
Report that this does not constitute a fresh full Docker validation.

## After

The migration remained attributable and runtime claims were stated at the
scope actually checked.

## Why

Combining behavior changes with structural movement makes regressions and
evidence ambiguous.

## Rejected alternatives

- Re-tune defaults during the move.
- Claim full runtime compatibility from static checks.
- Expand cleanup to unrelated files because they are nearby.

## Boundary

A behavior change required to make the requested migration coherent belongs in
scope, but its necessity and validation must be explicit.

## Evidence

The resulting review separated pre-existing runtime evidence from checks run on
the refactor diff.
