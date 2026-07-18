# C-028 Comments Explain Decisions

Related judgments: J-061
Source samples: 075

## Context

Hydra YAML comments varied between field-name repetition, stale default values,
and useful external constraints.

## Before

Comments increased maintenance cost without helping a reader decide how or why
to change configuration.

## Decision

Comment only information the schema cannot express: units, ownership, valid
ranges, upstream differences, coupling, and reasons for non-obvious defaults.
Keep comments beside the configuration domain that owns the decision.

## After

Configuration comments communicate design intent and can be checked against
the actual default rather than duplicating every field.

## Why

Syntax and field names are already visible; their rationale is not.

## Rejected alternatives

- Add a prose sentence for every YAML key.
- Copy default values into comments and documentation.
- Explain a model-specific constraint in an unrelated parent config.

## Boundary

Short labels may still aid navigation in a large file, but should not pretend to
document behavior.

## Evidence

The YAML documentation pass removed stale and redundant comments while retaining
constraints needed by users and maintainers.
