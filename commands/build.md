---
description: Run one specific prompt out of order — auth, analytics, offline, deploy…
argument-hint: "<topic or prompt number>  e.g. auth · 08 · offline · observability"
allowed-tools:
  - Bash
  - Read
  - Write
  - Edit
  - Glob
  - Grep
---

Invoke the `mobilekit` skill.

Run the prompt matching `$ARGUMENTS`, regardless of plan order. This is the escape hatch for existing projects and for one-off additions.

## Resolve the topic

Match `$ARGUMENTS` against the prompt index in the skill's SKILL.md and `mobilekit/README.md`. A number matches directly. A word matches by subject — "auth", "analytics", "offline", "deploy", "observability", "dark mode".

If the match is ambiguous — "auth" maps to both `04-authentication-clerk` and `05-authentication-database` — list the candidates in one line each and ask. Do not pick.

If nothing matches, say so and list the nearest three. Do not improvise a prompt that does not exist in the library.

## Check the prerequisites, then say so

Prompts assume things. Before running, state plainly what is missing rather than silently working around it:

- No `PRODUCT.md` → the prompt will have to guess the domain. Say that and recommend `/mobilekit:discovery`, but run it if the user confirms.
- A screen prompt with no `DESIGN.md` → the screen's empty / loading / error states are undefined. Ask for them inline and record the answers.
- `27-secure-backend-integration` is a prerequisite for anything holding a secret — AI, payments, realtime tokens. If the topic is one of those and 27 has not run, say so first.
- `34-post-release-observability` needs a production build with real users. Without one, thresholds are invented. Say so.

## Execute

Per the skill's "Executing a prompt" procedure. Verify installed versions. Ask the prompt's "Ask first" questions. Walk `Done when` and report honestly.

If `docs/BUILD-PLAN.md` exists and contains this step, check its box.
