# C-007 LoRA as a Nested Hydra Domain

Related judgments: J-012
Source samples: 061, 080

## Context

LoRA introduced rank, alpha, target modules, and export behavior into an already
composed model/actor configuration.

## Before

Fields could be flattened into a parent YAML or injected permanently with
Hydra `++`, creating duplicate or untyped override paths.

## Decision

Give LoRA an independent YAML config group and compose it under an explicit
nested package such as `lora@lora`. Translate to the upstream flattened schema
once at the typed consumer boundary.

## After

LoRA has one discoverable configuration path and the parent model configuration
does not duplicate its fields.

## Why

An independently meaningful and selectable domain deserves an independently
owned configuration group.

## Rejected alternatives

- Add each LoRA field directly to the actor YAML.
- Preserve both nested and flat aliases for convenience.
- Use permanent `++` overrides instead of declaring support.

## Boundary

Short-lived experiments may use Hydra additions before becoming supported API.

## Evidence

The same nested-group rule was generalized after inspecting the repository's
workflow YAML composition.
