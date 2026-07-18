# C-012 Remove AutoClass and Unused Compatibility

Related judgments: J-022, J-050
Source samples: 040, 071, 077

## Context

Central AutoClass registration imported unrelated model integrations. Legacy
aliases, `policy.`/`model.` prefix fallbacks, native-policy flags, old config
paths, and runtime patches remained after architecture changes.

## Before

A Pi0-only image could fail on an OpenVLA dependency. Several branches existed
for checkpoint or extension consumers that could not be identified.

## Decision

Use explicit model builders, remove central registration, and delete aliases,
fallback prefixes, completed migration paths, and patches without concrete
consumers.

## After

Loading a model imports only its integration. Every supported configuration and
checkpoint path is canonical and visible.

## Why

Disabled compatibility still expands dependencies, states, and required tests.

## Rejected alternatives

- Keep old names with deprecation comments indefinitely.
- Add optional flags around every runtime patch.
- Preserve both new and old config paths.

## Boundary

Compatibility is valid when a named external checkpoint, extension, or user
workflow requires it and the path is verified.

## Evidence

Repository searches found no consumers before removal; model-specific Docker
flows no longer imported unrelated dependencies.
