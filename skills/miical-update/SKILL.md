---
name: miical-update
description: Analyze the current conversation to explain why an initial request required follow-up instructions, diagnose whether Miical Code failed to constrain the agent, and propose a targeted improvement before applying it with approval. Use when the user asks to review a disappointing or fragmented interaction and evolve Miical Code from that evidence.
---

# Miical Update

Treat the current conversation as evidence for improving Miical Code. Separate
diagnosis, modification approval, and commit approval into distinct stages.

Resolve the canonical filesystem path of this `SKILL.md`; the Miical Code
repository is two directories above its containing skill directory. Modify that
source repository, not the user's target project or an installed copy.

## Diagnose and propose

Keep the first stage read-only. Do not edit, stage, commit, or change external
state before the user approves a concrete modification proposal.

1. Reconstruct the interaction:
   - identify the user's initial intended outcome;
   - identify what the agent completed in response;
   - list each follow-up instruction that corrected, clarified, or extended it;
   - describe the result that could reasonably have been completed from the
     initial request alone.
2. Classify why each follow-up was needed:
   - a necessary rule was absent from Miical Code;
   - an existing rule was too vague to produce an operational decision;
   - Miical Code did not trigger or did not load the relevant detail;
   - the agent failed to follow a rule that was already explicit; or
   - the user introduced a new preference or expanded scope that could not
     reasonably have been inferred.
3. Inspect the version of Miical Code that governed the interaction when it can
   be identified. Otherwise inspect the current source and state that limit.
   Read `skills/miical-code/SKILL.md`, the core profile files, and only the
   relevant detail files and cases. Check whether the desired behavior is
   already explicit before proposing another rule.
4. Decide whether the lesson generalizes. Do not add a repository rule for a
   one-off preference, a genuine scope change, or a compliance failure already
   covered clearly. When no justified repository change exists, say so rather
   than inventing one.
5. Choose the smallest semantic owner for each justified change:
   - use `skills/miical-code/SKILL.md` for loading or execution procedure;
   - use `profile/` for a reusable engineering judgment or style rule;
   - use `cases/` only for durable before-and-after evidence;
   - update other consumers only when the proposed rule changes them.

Present the first-stage response in the user's language with these sections:

- `Conversation gap`: initial outcome, actual response, and required follow-ups;
- `Root cause`: evidence-backed classification for each gap;
- `Miical Code gap`: the missing, vague, unloaded, or already-sufficient rule;
- `Proposed change`: exact behavior, affected files, and why it generalizes.

End by asking the user to confirm the proposed repository changes. Do not make
the changes in the same turn as the proposal.

## Apply after confirmation

Treat confirmation of the proposal as permission to modify only the approved
files and behavior. It is not permission to create a commit.

1. Refresh the repository status and source files. Preserve unrelated work. If
   the approved files or assumptions changed materially after the proposal,
   revise the proposal and request confirmation again.
2. Apply the smallest complete change. Update every direct consumer required
   to keep the rule discoverable and internally consistent.
3. Validate the affected Skills, links, formatting, and any behavior-specific
   checks. Report only checks that actually ran.
4. Explain what changed, where it changed, and what future agent decision is
   now different. Report remaining worktree changes.
5. Ask whether the user wants to prepare a local commit.

Do not stage or commit during this stage. If the user requests a commit, invoke
`$miical-commit` and follow its independent preview and final-confirmation
workflow.
