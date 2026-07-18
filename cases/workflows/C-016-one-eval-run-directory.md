# C-016 One Evaluation Run Directory

Related judgments: J-031, J-032
Source samples: 047, 053

## Context

Evaluation metrics, videos, logs, and model/cache data had separately configured
paths, sometimes placing video directly at repository root.

## Before

Users repeated coordinated paths in long commands and could create a run whose
artifacts were split across unrelated locations.

## Decision

Accept one evaluation `output_dir`. Derive `metrics.json`, a video subdirectory,
and run-specific artifacts beneath it. Keep persistent model/data cache separate
only because it has a different lifecycle.

## After

One directory is a complete evaluation result and can be inspected, archived,
or removed as a unit.

## Why

Related paths are derivable configuration, not independent user choices.

## Rejected alternatives

- Continue exposing `result_path` and `video.root` independently.
- Store videos at root for shorter paths.

## Boundary

Large shared datasets and model caches remain outside a run output because they
are reused and should not be deleted with one evaluation.

## Evidence

The eval YAML and launch command were reduced to one output root while metrics
and videos remained available in deterministic locations.
