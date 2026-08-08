---
description: Where this project is in the mobile workflow, and what to run next
allowed-tools:
  - Bash
  - Read
  - Glob
  - Grep
---

Invoke the `mobilekit` skill.

Read-only. Change nothing.

## Read

- `docs/PRODUCT.md` — exists? any `UNDECIDED` left?
- `docs/DESIGN.md` — exists? any screen with undefined states?
- `docs/BUILD-PLAN.md` — how many boxes checked of how many, and what the first unchecked one is
- `package.json` and the repo — does what is installed match what the plan claims is done? A checked box with no dependency installed is a lie in the file.

## Output

Short. No preamble.

```
Phase:      [discovery | design | build | ship | observe]
PRODUCT.md  ok · 2 UNDECIDED
DESIGN.md   missing
BUILD-PLAN  7/21 · next: 16 — tab navigation
Drift:      plan says 07-zustand done, zustand not in package.json
Next:       /mobilekit:design
```

Report drift when the files and the repo disagree. Do not fix it — say which one is wrong and let the user decide.

If none of the three files exist, say the project has not started this workflow and point at `/mobilekit:init`.
