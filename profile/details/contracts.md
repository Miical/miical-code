# Data, State, and Configuration Contracts

## J-010 Trace values to their producer

When a tensor shape, numerical range, task identifier, or configuration value
is unclear, inspect where it is produced and transported. Establish the
correct form there before editing the consumer. A consumer should not infer
whether an action is two- or three-dimensional or whether an image is uint8 or
normalized float.

## J-011 Use one canonical representation and parse path

Choose one representation for each supported source and normalize at its
boundary. Downstream code uses one access path. Conditional parsing is valid
only when the supported sources and their distinct schemas are named, as with
simulator uint8 images and normalized dataset images.

Reject unknown forms instead of adding fallback prefixes, keys, shapes, or
attribute locations. Defensive acceptance makes contract violations harder to
locate.

## J-012 Declare supported configuration explicitly

Stable behavior belongs in typed configuration. An independently meaningful
domain such as LoRA, simulator, recorder, or adapter gets its own Hydra group
and explicit nested package. Do not flatten its fields into a parent or expose
parallel aliases.

If an upstream component consumes a different schema, translate once at the
typed ownership boundary. Runtime `++` additions are for temporary experiments,
not a permanent API.

## J-013 Derive rather than duplicate state

Do not store both epoch and step when one determines resumption, both enable
and a nullable value when the value determines enablement, or both primitive
records and mutable aggregates when aggregates can be computed.

Choose the state that determines future behavior. Derive display values and
summaries from it.

## J-014 Keep runtime data out of native artifact configuration

Upstream model configuration describes the upstream model. Dataset statistics,
local paths, embodiments, critic settings, and workflow options belong to the
integration or runtime. Pass them explicitly and save required sidecars beside
the exported artifact without rewriting the native configuration schema.
