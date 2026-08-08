---
description: Install the mobilekit prompt library into this project and write AGENTS.md
allowed-tools:
  - Bash
  - Read
  - Write
  - Edit
  - Glob
---

Invoke the `mobilekit` skill, then do the following.

## 1. Inspect before writing

- Is this an Expo project? Read `package.json`. If there is no `expo` dependency, say so and ask whether to scaffold (`3-foundation/01-expo-project-setup.md`) or whether this is the wrong directory.
- Does `mobilekit/` already exist in this project (`mobilekit/RULES.md` exists)? If yes, **do not overwrite**. List which files differ from the skill's `prompts/` and ask what to do. A project may have customized its copy on purpose.
- Does `AGENTS.md` or `CLAUDE.md` already exist? Read it. You are extending it, not replacing it.

## 2. Install the library

Copy `~/.claude/skills/mobilekit/prompts/` into this project's `mobilekit/`. Everything after this point reads from the project's copy, not from the skill — the project owns it and may edit it.

## 3. Write AGENTS.md

Follow `mobilekit/1-discovery/00-agents-md-guide.md`.

If `docs/PRODUCT.md` does not exist yet, write only the parts that are true regardless of the product — stack, folder layout as actually found in the repo, conventions read from existing code — and mark the product-specific sections `TBD — run /mobilekit:discovery`. Do not invent the domain to fill them.

## 4. Report

State what was copied, what was left alone, and what the next command is:

- No `PRODUCT.md` → `/mobilekit:discovery`
- `PRODUCT.md` exists → `/mobilekit:design`
