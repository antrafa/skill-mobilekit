---
description: Run the next unchecked step of docs/BUILD-PLAN.md
allowed-tools:
  - Bash
  - Read
  - Write
  - Edit
  - Glob
  - Grep
---

Invoke the `mobilekit` skill.

**Prerequisite:** `docs/BUILD-PLAN.md`. Missing → say to run `/mobilekit:plan`.

## Run one step

1. Read `BUILD-PLAN.md` and take the **first unchecked box**. One step. Do not run ahead into the next one because it looks small.
2. Announce which step and which prompt file, and give the user a chance to skip it before you start.
3. Execute it per the skill's "Executing a prompt" procedure: read `RULES.md`, `PRODUCT.md`, `DESIGN.md`, `AGENTS.md`; follow the prompt's `## Prompt` section as written; ask its "Ask first" questions rather than answering them yourself.
4. Verify the installed version of anything you configure against `package.json` and that version's docs. Do not write setup from memory.
5. Walk the `Done when` checklist and report each item met / not met / not verifiable. Do not tick a box you did not test.
6. Check the box in `BUILD-PLAN.md` only if the checklist actually passed. Partially done stays unchecked, with a note of what remains.

## Blocked

If the step cannot proceed — a missing account, an `UNDECIDED` in `PRODUCT.md`, a credential you must not create — stop, say exactly what is needed from the user, and leave the box unchecked. Do not substitute a placeholder and move on.

## Report

What was built, what the checklist says, and what the next unchecked step is.
