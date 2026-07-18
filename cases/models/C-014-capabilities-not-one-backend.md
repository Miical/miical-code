# C-014 Capabilities, Not One Backend Format

Related judgments: J-020, J-024
Source samples: 043

## Context

Future integrations included ACT, SmolVLA, LingBot, Xiaomi VLA, Pi0, GR00T, and
OpenVLA across LeRobot, Diffusers, Transformers, and custom PyTorch.

## Before

A proposed Backend taxonomy attempted to standardize loading and export before
the real model integrations shared one implementation contract.

## Decision

Keep explicit integration builders and native policy lifecycle. Let TrainableModel
classes declare supported capabilities such as SFT, action sampling, or critic.
Let trainers depend on capabilities rather than model names.

## After

Models may preserve different native formats while participating in the same
training and execution framework.

## Why

The stable commonality is what the framework can ask a model to do, not which
third-party library stores it.

## Rejected alternatives

- Require every policy to implement Transformers AutoModel.
- Create one Backend class per third-party library as a prerequisite.
- Branch trainers on concrete model names.

## Boundary

An integration may internally factor repeated native loading code when several
real models use it, without making that factor a core framework requirement.

## Evidence

Pi0 and GR00T shared the TrainableModel lifecycle while retaining Diffusers and
Transformers exports respectively.
