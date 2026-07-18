# C-021 Four Teleop Latency Measures

Related judgments: J-041, J-044
Source samples: 063, 084

## Context

Interactive teleoperation felt slow, with possible causes in simulation, JPEG
and Base64 encoding, WebSocket publication, and recording.

## Before

Optimization ideas targeted several components without evidence about their
share of end-to-end latency.

## Decision

Measure only `env_step_ms`, `teleop_publish_ms`, `record_ms`, and `total_ms`
behind a simple log switch. Place each timer at the operation's owning boundary.

## After

Measurements showed environment steps around 163-165 ms while publication and
recording were about 1-2 ms each, moving optimization attention to simulation.

## Why

Four attributable values were enough to reject the main incorrect hypotheses.

## Rejected alternatives

- Add a general tracing platform before locating the bottleneck.
- Rewrite image transport first because it was easier to change.
- Collect many metrics with no corresponding decision.

## Boundary

After the dominant stage is found, its internal distribution can be measured in
a separate focused investigation.

## Evidence

Real EnvWorker log lines made the stage contribution directly comparable.
