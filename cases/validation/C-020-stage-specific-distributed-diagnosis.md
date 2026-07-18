# C-020 Stage-Specific Distributed Diagnosis

Related judgments: J-041
Source samples: 048, 062

## Context

Docker builds and distributed evaluation were described as slow or stuck while
failures occurred in several unrelated systems.

## Before

Registry authentication, network transfer, full disk, Ray actor creation,
TCPStore rendezvous, model download, and environment startup produced similar
high-level symptoms.

## Decision

Identify the last completed stage, inspect that owner's logs and state, and
classify the failure before changing code. Treat registry, network, storage,
process group, model load, and environment step as distinct boundaries.

## After

401 registry errors, no-space failures, and TCPStore failures received different
fixes rather than a shared speculative workaround.

## Why

The symptom "stuck" contains no ownership information.

## Rejected alternatives

- Add more timeouts or dependencies everywhere.
- Change model code while the disk is full.
- Assume a long startup is an environment-step performance bug.

## Boundary

Once a stage is identified, deeper instrumentation may be added narrowly at its owner.

## Evidence

Disk and Docker cache inspection found zero free root space in one run; Ray logs
located process-group initialization in another.
