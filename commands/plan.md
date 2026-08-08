---
description: Turn PRODUCT.md + DESIGN.md into an ordered build checklist → docs/BUILD-PLAN.md
allowed-tools:
  - Bash
  - Read
  - Write
  - Edit
  - Glob
  - Grep
---

Invoke the `mobilekit` skill.

**Prerequisite:** `docs/PRODUCT.md`. `docs/DESIGN.md` is strongly preferred — without it the screen steps are guesses. If it is missing, say so and ask whether to run `/mobilekit:design` first or to plan the non-screen work only.

## Build the plan

Start from the reference order in `mobilekit/README.md`, then **cut it down**:

- Remove every step whose capability `PRODUCT.md` marks "later" or "never". No payments step for an app with no payments.
- Replace the generic screen steps with the actual screens from `DESIGN.md`, in its build order — core screens first.
- Choose between mutually exclusive prompts and say why in one line: Clerk (04) vs own backend (05); Supabase (06) vs an existing API; React Query (12) only if data comes from a remote source.
- Read the repo. Anything already done gets marked done, not queued. Check `package.json` and the actual files, not assumptions.

## Output

Write `docs/BUILD-PLAN.md`:

```markdown
# Build Plan

Generated from PRODUCT.md and DESIGN.md. `/mobilekit:next` runs the first unchecked step.

## Foundation
- [x] 01 — Expo project setup · already present
- [ ] 02 — NativeWind
- [ ] 05b — Domain model

## Screens
- [ ] 17 — [real screen name from DESIGN.md]

## Release
- [ ] 33 — Accessibility audit
- [ ] 26 — EAS build & deploy

## Skipped
| Step | Why |
|---|---|
| 13 — RevenueCat | PRODUCT.md: payments = never |
```

Every unchecked box is one prompt file. Never merge two prompts into one box — `/mobilekit:next` runs one at a time on purpose.

## Report

Show the plan, the count of steps, and what was skipped. Then point at `/mobilekit:next`.
