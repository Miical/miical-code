# Case Index

These are curated decision cases used by `miical-code`. They are evidence for
the profile judgments, not an additional source of rules. Read a case when its
linked judgment materially affects the current task or its boundary is unclear.

Raw extraction remains in [`../sample/`](../sample/) and is not loaded during
normal skill use.

## Architecture

- C-001 — EntryPoint, Workflow, Trainer, and TrainCluster ownership
- C-002 — Recorder domain behavior moved out of `utils`
- C-003 — Checkpoint and resume state have one owner
- C-025 — A refactor changes only its authorized scope
- C-026 — Repository operations preserve unrelated work
- C-027 — A cross-machine handoff records executable state

## Contracts

- C-004 — Reset states use one canonical tuple
- C-005 — Image normalization follows explicit producer contracts
- C-006 — Dataset normalization statistics stay outside native model config
- C-007 — LoRA is an explicit nested Hydra domain
- C-008 — Primitive trajectory facts precede aggregates

## Models

- C-009 — Native Policy and TrainableModel produce distinct artifacts
- C-010 — Export behavior stays on the owning base class
- C-012 — AutoClass registration and unused compatibility are removed
- C-013 — Critic reuse stops at the stable semantic boundary
- C-014 — Model integrations share capabilities, not one backend format

## Workflows

- C-015 — Pi0.5 exposes one minimal supported launcher
- C-016 — Evaluation outputs derive from one run directory
- C-017 — RECAP and standalone evaluation share one workflow

## Validation and runtime

- C-018 — LIBERO install validation performs real CPU rendering
- C-019 — Pi0.5 Docker completion requires real optimizer steps
- C-020 — Distributed startup is diagnosed stage by stage
- C-021 — Four latency measurements identify the real bottleneck
- C-022 — Tests protect meaningful behavior, not every helper
- C-023 — WebRTC is rejected after a measured cost-benefit review

## Evolution and readability

- C-011 — Early stopping remains a small state abstraction
- C-024 — Failed experiments and completed migrations leave no residue
- C-028 — YAML comments explain decisions rather than fields
