# C-022 Selective Behavior Tests

Related judgments: J-043
Source samples: 021, 025, 068

## Context

Agents repeatedly added tests for prompts, helpers, forwarding layers, config
defaults, and speculative defensive branches.

## Before

Test count increased while implementation details became harder to refactor.
Important mathematical and multi-environment behavior still needed precise proof.

## Decision

Test complete, independently meaningful behavior: advantage formulas and tail
boundaries, computed statistics, multi-environment intervention/exit transitions,
scheduling, resume, and checkpoint export/reload. Remove tests for trivial
prompts, private call order, and unsupported fallbacks.

## After

Tests protect durable semantics without forcing unnecessary abstractions or
compatibility.

## Why

Tests are maintained contracts. Incidental contracts reduce design freedom.

## Rejected alternatives

- Add a test for every changed helper.
- Maximize line coverage regardless of semantic value.
- Avoid testing complex formulas because the implementation is short.

## Boundary

Simple code still deserves a test when it implements a high-impact external or
mathematical contract.

## Evidence

Formula and multi-env regression tests caught real behavior risks; low-value
early-stop/prompt tests were deliberately removed.
