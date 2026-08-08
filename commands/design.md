---
description: Design conception — screens, navigation, per-screen states, visual direction → docs/DESIGN.md
allowed-tools:
  - Bash
  - Read
  - Write
  - Edit
  - Glob
  - Grep
---

Invoke the `mobilekit` skill.

**Prerequisite:** `docs/PRODUCT.md`. If it does not exist, stop and say to run `/mobilekit:discovery` first — there is nothing to derive screens from.

## Step 1 — Structure

Run `mobilekit/2-design/00c-design-conception.md`. Write no code and install nothing; the only output is `docs/DESIGN.md`.

Every screen must trace to a core-journey step or a capability marked "now" in `PRODUCT.md`. Use the domain vocabulary from `PRODUCT.md`, never generic nouns.

## Step 2 — Visual system

Only after `DESIGN.md` records a visual direction, run `mobilekit/2-design/03-design-system.md` to turn it into tokens.

If the user has a design reference (Figma export, screenshots), ask for it before proposing anything: `@path/to/reference.png`. If not, propose directions and **let the developer choose the palette** — do not pick one for someone's product.

If `$ARGUMENTS` names a specific concern (e.g. "só as telas", "só os tokens"), run only that step.

## Report

Say which screens were dropped and why, what is still `UNDECIDED`, and point at `/mobilekit:plan`.
