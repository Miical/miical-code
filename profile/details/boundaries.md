# Boundaries and Ownership

## J-001 Place behavior with its semantic owner

Ask three questions: who defines the behavior's meaning, who owns its
lifecycle, and which component has all information required to decide? Put the
behavior at the lowest layer for which all three answers are coherent.

Examples: workflows own cross-stage orchestration; trainers own algorithm
progression; TrainCluster owns distributed topology and worker lifecycle;
environments own simulator task identity; model integrations own policy input
and output translation.

Do not classify code by its current caller. A workflow may call a return
computation without making that computation a trainer responsibility.

## J-002 Preserve one-way dependency direction

Dependencies should follow orchestration toward execution:

```text
examples/docs -> entrypoints -> workflows -> trainers/TrainCluster
             -> workers -> models/envs
```

When a lower layer needs behavior currently found above it, extract the
required capability to a lower owner or pass the result down. Do not import a
workflow merely to reuse a helper.

## J-003 Give lifecycle state one owner

Resources, checkpoints, progress, and mutable session state need a single
owner. Other layers request operations or read derived views. Construct
optional lifecycle helpers when their configuration is accepted; avoid later
`init_*` calls and guards that create partially initialized states.

Store only the values needed to determine future behavior. Prefer a property
over a second mutable copy of a derivable path or status.

## J-004 Keep domain behavior out of generic utilities

A utility is small, stateless, and shared across multiple domains. Code that
understands a dataset format, simulator backend, recording lifecycle, policy
artifact, or configuration domain belongs with that domain even when several
callers use it.

Moving domain code into `utils` hides ownership and invites unrelated callers.
Extract a public domain operation instead.
