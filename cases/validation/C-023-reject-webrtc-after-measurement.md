# C-023 Reject WebRTC After Measurement

Related judgments: J-044
Source samples: 089, 090, 091, 093

## Context

WebRTC was considered to reduce teleoperation video latency.

## Before

WebSocket carried Base64 JPEG and could queue stale frames, but timing also
showed simulator step dominated the budget.

## Decision

First remove Base64, send binary JPEG, encode off the step path, and use a
bounded latest-frame-wins preview queue. Reject WebRTC because signaling, peer
lifecycle, and deployment complexity did not address the dominant bottleneck.

## After

The system kept a smaller transport protocol with fresher frames and removed
the WebRTC experiment and its residue.

## Why

A more capable protocol is not automatically a better system choice.

## Rejected alternatives

- Adopt WebRTC because it is designed for media.
- Keep experimental WebRTC behind a disabled option.
- Degrade image quality substantially without evidence it dominates latency.

## Boundary

WebRTC becomes appropriate if measured media transport, congestion, or browser
decode—not simulator execution—becomes the limiting requirement.

## Evidence

Stage timings and the simpler transport improvements established the actual
cost-benefit boundary.
