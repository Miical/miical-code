# Naming and Explanation

## J-060 Name by responsibility and user intent

Internal names should identify the domain role: `train_cluster`,
`collect_data`, or `compute_return`. Public names should identify what the user
does: `run_train` or `run_eval`. Avoid vague names such as `runner`, historical
implementation names, and repeated context such as `envs/libero_env.py`.

Renaming is part of a responsibility migration. Update callers and docs rather
than preserving unused aliases.

## J-061 Explain decisions, not syntax

Comments explain constraints the code cannot express: units, ownership,
external compatibility, tradeoffs, and why a non-obvious choice is required.
Documentation explains the supported workflow and verified behavior. Do not
repeat field names, visible defaults, or line-by-line execution.
