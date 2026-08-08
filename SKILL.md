---
name: mobilekit
description: Guided end-to-end workflow for building React Native / Expo mobile apps — product discovery, design conception, implementation, release, and post-release observability. Use when the user is starting a mobile app, asks what to build next in an Expo project, or invokes any /mobilekit:* command. Carries a phase-organized prompt library covering auth, state, backend, AI, analytics, payments, screens, i18n, offline, testing, accessibility, EAS deploy and monitoring.
---

# mobilekit

A phase-driven workflow over a prompt library. The library lives in `prompts/` next to this file; the target project gets its own copy at `mobilekit/` once `/mobilekit:init` runs.

The value of this skill over reading the files directly is that it knows **where the project is** in the build and refuses steps whose prerequisites are missing.

## Layout in a project

The library and the documents it produces are deliberately separate. `PRODUCT.md` is read by people who do not know this skill exists.

```
mobilekit/            the prompt library (copied by /mobilekit:init)
  RULES.md            read before every prompt
  README.md           index + reference build order
  1-discovery/  2-design/  3-foundation/  4-platform/
  5-screens/    6-features/  7-ship/      8-observability/

docs/                 what the workflow produces
  PRODUCT.md          /mobilekit:discovery
  DESIGN.md           /mobilekit:design
  DOMAIN.md           05b-domain-model
  BUILD-PLAN.md       /mobilekit:plan
```

Folder numbers are phase order. **File numbers are stable IDs** — `05b-domain-model.md` keeps that name wherever it sits, so `BUILD-PLAN.md` entries and prose cross-references between prompts survive reorganization. Never renumber a file.

## State

The presence of the three documents *is* the phase:

| File | Written by | Means |
|---|---|---|
| `docs/PRODUCT.md` | `/mobilekit:discovery` | The product is defined. Nothing else may run before this exists. |
| `docs/DESIGN.md` | `/mobilekit:design` | Screens, navigation and per-screen states are decided. |
| `docs/BUILD-PLAN.md` | `/mobilekit:plan` | An ordered checklist of only the steps this app needs. This is the progress tracker. |

Never guess at a missing one. If `PRODUCT.md` is absent, the answer to almost any `/mobilekit:*` command is "run `/mobilekit:discovery` first".

## Hard rules

These override the general instinct to be helpful by filling gaps:

1. **Never invent the domain.** Not from the folder name, not from an existing template, not from a scaffold. A repo cloned from a tutorial tells you nothing about the product.
2. **Never decide an `UNDECIDED`.** Ask, then update the file that records it.
3. **Verify the installed version before writing setup code.** Read `package.json`, then that version's docs via context7 or the official URL. Config layout moved in Tailwind 3→4, NativeWind 4→5, Reanimated 3→4, Sentry 7→8. Setup pasted from memory is the most common failure here.
4. **Inspect the repo before creating files.** `app/` or `src/app/`? Does `babel.config.js` exist? Follow what is there. Paths in the prompts are illustrative.
5. **Options are questions.** Where a prompt offers Option A / B / C, present them and recommend one in a line. Do not choose silently.
6. **Secrets stay server-side.** `EXPO_PUBLIC_*` ships inside the bundle and is public by definition. Never commit keys or `.env`.
7. **Skip what `PRODUCT.md` marks "later" or "never"** — no prompt run, no dependency installed.
8. **Report honestly.** What was skipped, what was assumed, what could not be verified. A failed step means showing the output.

## Executing a prompt

Every prompt file has the same shape: a header explaining when it applies, a `## Prompt` section, and a `### Done when` checklist.

1. Read `mobilekit/RULES.md`, `docs/PRODUCT.md`, `docs/DESIGN.md` (if it exists) and `AGENTS.md`.
2. Read the prompt file and follow its `## Prompt` section **as written** — it is the instruction, not a summary to paraphrase.
3. Answer its "Ask first" block by asking the user. Do not answer it on their behalf.
4. Build.
5. Walk its `Done when` checklist and report each item as met, not met, or not verifiable. Do not tick a box you did not test.
6. If `docs/BUILD-PLAN.md` exists, mark that step done in it.

## Phase map

```
idea      → /mobilekit:discovery   1-discovery/00-product-discovery   → docs/PRODUCT.md
            /mobilekit:init        1-discovery/00-agents-md-guide     → AGENTS.md + mobilekit/
design    → /mobilekit:design      2-design/                          → docs/DESIGN.md
plan      → /mobilekit:plan        (reads both)                       → docs/BUILD-PLAN.md
build     → /mobilekit:next        the next unchecked step
            /mobilekit:build <x>   one step, out of order
ship      → /mobilekit:ship        7-ship/ + 8-observability/09       → release gate
observe   → /mobilekit:build 34    8-observability/34                 → after real users
```

`/mobilekit:status` reads the three documents and says where the project is.

## Finding a prompt

Glob `mobilekit/**/<number>-*.md` — file numbers are unique across the library, so a number alone resolves. By phase:

| Folder | Contains |
|---|---|
| `1-discovery` | 00-product-discovery, 00-agents-md-guide |
| `2-design` | 00c-design-conception, 03-design-system |
| `3-foundation` | 01-expo-project-setup, 02-nativewind-setup, 05b-domain-model, 24-common-ui-components |
| `4-platform` | 04-authentication-clerk, 05-authentication-database, 06-supabase-setup, 07-zustand-setup, 12-react-query, 27-secure-backend-integration |
| `5-screens` | 15-onboarding, 16-tab-navigation, 17-home, 18-detail, 19-profile, 20-settings, 21-form, 22-list, 23-modal-bottom-sheet |
| `6-features` | 10-push-notifications, 11-reanimated, 13-revenuecat, 14-payment-gateway, 25-dark-mode, 28-ai-features, 29-internationalization, 31-offline-support, 32-deep-linking |
| `7-ship` | 30-testing, 33-accessibility-audit, 26-eas-build-deploy |
| `8-observability` | 08-posthog-analytics, 09-sentry-error-tracking, 34-post-release-observability |

Full descriptions and the reference build order: `mobilekit/README.md`.
