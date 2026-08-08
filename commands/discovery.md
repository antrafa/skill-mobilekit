---
description: Product discovery interview — defines what the app is, writes docs/PRODUCT.md
allowed-tools:
  - Bash
  - Read
  - Write
  - Edit
  - Glob
  - Grep
---

Invoke the `mobilekit` skill, then run `mobilekit/1-discovery/00-product-discovery.md` (or `~/.claude/skills/mobilekit/prompts/1-discovery/00-product-discovery.md` if the project has no copy yet).

Follow it exactly. In particular:

- **Write no application code and install nothing.** The only file produced is `docs/PRODUCT.md`.
- Ask in batches of 3 to 5 with a recommended default for each. Do not dump the questionnaire at once.
- Never infer the domain from the folder name, the repo, or an existing scaffold.
- Anything unresolved is recorded literally as `UNDECIDED — ask before assuming`.

If `docs/PRODUCT.md` already exists, read it first and ask whether this is a revision of specific sections or a fresh start. Do not silently overwrite a document the developer answered by hand.

When done, point at `/mobilekit:design`.
