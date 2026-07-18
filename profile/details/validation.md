# Evidence, Reliability, and Performance

## J-040 Prove the real execution closure

Choose the smallest execution that contains the behavior being claimed. A
LIBERO environment check creates, resets, steps, and renders. A training check
loads the real model and data and completes an optimizer step. Artifact
compatibility requires export and reload through the intended implementation.

## J-041 Diagnose from stage-specific evidence

Locate the failing stage before editing: registry resolution, download,
dependency installation, actor creation, process-group rendezvous, model load,
dataloader, environment step, encoding, or cleanup. Inspect logs and state from
that owner. Change one supported boundary at a time.

## J-042 Match the claim to the validation scope

Static imports can prove a refactor did not leave obvious references; they
cannot prove Docker runtime behavior. State known baselines separately from
checks executed after a change. Explicitly report unverified boundaries.

## J-043 Test only durable, meaningful behavior

Add dedicated tests for independently meaningful logic whose regression would
be costly: formulas, dataset statistics, multi-environment state transitions,
scheduling, resumption, and artifact round trips. Do not test every private
helper, forwarding call, default value, or unsupported fallback.

## J-044 Measure before optimizing

Define a small set of attributable timings around real owners. Optimize the
dominant cost while preserving required quality and semantics. If an
experiment does not show material end-to-end benefit, remove it and its
configuration rather than keeping it disabled.
