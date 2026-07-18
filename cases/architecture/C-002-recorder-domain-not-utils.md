# C-002 Recorder Domain, Not Utilities

Related judgments: J-001, J-002, J-004
Source samples: 032, 038

## Context

LeRobot dataset merge, truncate, metadata, episode, and output-recovery logic
was stored under `utils/recorder`.

## Before

The location suggested stateless generic helpers even though the code knew the
Recorder data format and was used by recording and collection workflows.

## Decision

Move dataset-format and recording-output behavior into the `recorder` domain.
Keep RECAP-specific orchestration, such as computing returns and merging the
training dataset for a stage, in the RECAP workflow.

## After

Recorder owns reusable LeRobot recording operations. Workflows compose those
operations for their algorithm-specific purpose. Generic `utils` remains small.

## Why

Shared use does not make code generic. Knowledge of a domain format is a clear
ownership signal.

## Rejected alternatives

- Leave everything under `utils` because several callers use it.
- Move RECAP return computation into Recorder because it edits Recorder output.

## Boundary

Small stateless helpers that neither understand Recorder semantics nor own a
lifecycle may remain in common utilities.

## Evidence

The migration removed reverse dependencies and left each operation with callers
that depend in one direction.
