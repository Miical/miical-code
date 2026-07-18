# Abstraction and Reuse

## J-020 Abstract only after real repetition

Require more than a predicted need. Identify at least two real implementations,
their consumers, and the behavior that remains invariant across them. If the
variation is still changing, keep the implementations explicit until the
contract becomes visible.

## J-021 Use the smallest abstraction that owns the behavior

A base-class method is preferable to a separate exporter hierarchy when every
trainable model already owns native export. A small state object is preferable
to a result model plus several policy classes when the behavior is one window
and one stop decision.

Choose the smallest construct that gives the behavior a clear name, owner, and
test boundary.

## J-022 Add compatibility only for an identified consumer

Compatibility has a cost even when disabled. Name the checkpoint, extension,
external caller, or migration window that requires it. Cover that path with an
appropriate check. Without a consumer, remove aliases, prefix fallbacks,
monkey patches, and old configuration paths.

## J-023 Reuse contracts, not names

Two critics may share attention or MLP mathematics while requiring different
policy features and action encodings. Two adapters may both translate actions
while having no stable shared implementation. Reuse the mathematical or
lifecycle core only where inputs, outputs, and ownership match.

## J-024 Preserve upstream-native implementations and formats

The framework may standardize training capabilities and distributed execution
without standardizing every model library. Keep the upstream policy loadable
and exportable through its authors' implementation. Wrap it for training and
store auxiliary state in the full training checkpoint.
