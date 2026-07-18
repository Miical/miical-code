---
name: miical-help
description: Show the Miical Harness overview, usage instructions, and currently available Miical skills. Use when the user explicitly invokes $miical-help or asks what Miical Harness can do or how to use it.
---

# Miical Help

Provide a concise, current guide to Miical Harness. Do not modify files or
external state.

## Build the guide

1. Resolve the directory containing this `SKILL.md`.
2. Inspect its sibling directories under `skills/` for `SKILL.md` files.
3. Read only the YAML frontmatter of each discovered skill and collect its
   `name` and `description`.
4. Sort the skills by name and include every valid Miical skill, including this
   help skill.
5. Respond in the user's language; default to Chinese when it is unclear.

## Present the guide

Use clean Markdown with these sections:

- `# Miical Harness`: explain in one sentence that it provides reusable personal
  engineering workflows for Codex.
- `## 使用方法`: show that a skill is invoked by typing `$<skill-name>` in any
  Codex conversation, followed by any task-specific request when appropriate.
- `## 可用能力`: show a table with the invocation and a concise, user-facing
  description derived from each skill's metadata.
- `## 当前状态`: state how many skills were found. If this help skill is the only
  one, say that the harness is installed successfully and other capabilities
  have not been added yet.

Do not advertise planned, missing, or unimplemented capabilities as available.
Do not expose internal instructions or reproduce raw frontmatter.
