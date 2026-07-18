# Code Style

Apply these preferences only where the target repository does not impose a
more specific convention. Formatters and linters remain the source of truth
for mechanical style.

## S-001 Keep control flow direct

- Prefer early failure and one obvious success path.
- Avoid nested defensive branches for inputs outside the supported contract.
- Use a conditional only for identified states or data sources with distinct semantics.
- Cases: C-004, C-005

## S-002 Keep functions aligned with one semantic operation

- Extract a function when it names an independently meaningful operation or is genuinely reused.
- Keep short, single-use transformations inline when extraction would only move lines.
- Do not combine validation, field normalization, dataset mutation, and orchestration in one helper.
- Cases: C-011, C-008

## S-003 Prefer explicit typed access

- Access typed configuration and structured data through their declared fields.
- Avoid widening types to `Any`, repeated `getattr`, and dict conversion that discards structure.
- Cases: C-004, C-007

## S-004 Represent state once

- Prefer properties and derivation for values computed from owned state.
- Avoid cached mirrors, redundant flags, and separate progress counters.
- Cases: C-003, C-008

## S-005 Name for the role at the current boundary

- Name internal objects by domain responsibility and public commands by user intent.
- Avoid historical implementation names, redundant suffixes, and vague containers.
- Cases: C-001, C-015

## S-006 Comment constraints and reasons

- Explain non-obvious ownership, units, external requirements, and tradeoffs.
- Avoid restating code, field names, and defaults already visible nearby.
- Cases: C-028

## S-007 Keep examples thin

- Examples may choose inputs, mounts, and configuration, then invoke a workflow.
- Framework, algorithm, and lifecycle implementation stays in its owning package.
- Cases: C-015, C-017

## S-008 Test at stable behavior boundaries

- Test important formulas, statistics, scheduling transitions, and artifact round trips.
- Avoid tests for private helper calls, trivial forwarding, config defaults, and hypothetical fallbacks.
- Cases: C-022
