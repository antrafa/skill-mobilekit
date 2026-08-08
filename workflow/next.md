# Phase — next

Run the first unchecked step of the plan. Alias: `/mobilekit:next`.

**Prerequisite:** `docs/BUILD-PLAN.md`. Missing → run the plan phase.

## Run one step

1. Read `BUILD-PLAN.md` and take the **first unchecked box**. One step. The next one stays untouched however small it looks.
2. Announce which step and which prompt file, and give the developer a chance to skip it before starting.
3. Execute it per the skill's "Executing a prompt" procedure: read `prompts/RULES.md`, `docs/PRODUCT.md`, `docs/DESIGN.md`, `AGENTS.md`; follow the prompt's `## Prompt` section as written; work its `### Grill` block one question at a time.
4. Resolve the installed version of anything you configure against `package.json`, and get that version's docs per `prompts/RULES.md` §3.
5. Walk the `Done when` checklist and report each item met / not met / not verifiable. A box you did not test stays unticked.
6. Check the box in `BUILD-PLAN.md` only when the checklist actually passed. Partially done stays unchecked, with a note of what remains.

## Blocked

A step that cannot proceed — a missing account, an `UNDECIDED` in `PRODUCT.md`, a credential you must not create — stops, states exactly what is needed from the developer, and leaves the box unchecked. A placeholder substituted to keep moving is a bug shipped with a tick beside it.

## Report

What was built, what the checklist says, and the next unchecked step.
