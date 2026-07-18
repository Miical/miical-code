# User Workflows and Interfaces

## J-030 Expose one minimal entrypoint

Name entrypoints after user goals such as `run_train` and `run_eval`. Expose
only values the user must choose. Hide Hydra composition, dependency
workarounds, worker construction, and internal helper scripts behind that
boundary.

Minimal does not mean guessing prerequisites. Use standard loading mechanisms
and fail clearly when a required artifact is absent.

## J-031 Maintain one supported workflow

Prefer one path that is continuously exercised over Docker/native/legacy paths
that drift independently. A local expert can reconstruct an environment from
the authoritative Docker definition without the project promising a second
maintained workflow.

## J-032 Derive related outputs from one run root

Configure one output directory and derive metrics, video, logs, checkpoints,
and other run artifacts beneath it. Do not ask users to repeat coordinated
paths. Use a separate persistent data/cache root only when its lifecycle is
meaningfully different from a run output.

## J-033 Keep orchestration out of examples and entrypoints

Examples select supported configuration and invoke an entrypoint. Entrypoints
select a workflow. Workflows create and clean up clusters, coordinate stages,
and call trainers. Do not implement models, datasets, algorithms, or worker
lifecycle in user-facing scripts.
