# C-027 Executable Handoff

Related judgments: J-054
Source samples: 069, 070

## Context

GR00T Arena bring-up moved from an H20 machine to a 4090 machine because of
driver and environment constraints.

## Before

Critical state lived in a long conversation: PR branch, submodule state,
BuildKit issues, image status, driver requirements, and the next verification.

## Decision

Write a repository handoff containing the objective, current branch and PR,
completed evidence, exact blocker, hardware requirements, paths, next commands,
success criterion, and remaining work.

## After

The next machine can continue from authoritative state without reconstructing
the entire conversation.

## Why

A handoff exists to enable the next action, not to narrate the previous effort.

## Rejected alternatives

- Paste the full chat transcript.
- Report only that the first machine was incompatible.
- Rely on a future agent to rediscover image and checkpoint state.

## Boundary

Short same-session tasks do not need a handoff artifact; cross-machine or long
running work does.

## Evidence

The handoff recorded the real episode goal and separated completed environment
work from the remaining 4090 validation.
