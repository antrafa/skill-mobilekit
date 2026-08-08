---
description: Pre-release gate — testing, accessibility, error tracking, secret leaks, then EAS build
allowed-tools:
  - Bash
  - Read
  - Write
  - Edit
  - Glob
  - Grep
---

Invoke the `mobilekit` skill.

This is a gate, not a step. It runs several prompts in a fixed order because each one finds problems that are cheaper before submission than after.

## Order

1. **`7-ship/30-testing.md`** — risk-driven scope. If the app handles money or auth, this is not optional.
2. **`7-ship/33-accessibility-audit.md`** — a cross-app sweep. Store review rejects on this; users leave over it.
3. **`8-observability/09-sentry-error-tracking.md`** — if it has not run. Shipping without it means the first production crash is invisible.
4. **`7-ship/26-eas-build-deploy.md`** — profiles, environment variables, submission.

Skip a step only if the user says to, and record it in the report as skipped rather than passed.

## Secret leak check — do this before the first store build

Not a paste from memory, an actual check:

- `git ls-files` for anything credential-shaped: `.env`, `*.p8`, `*.p12`, service-account JSON, keystores. The Google Play service-account JSON and Firebase's `google-services.json` are different files and get confused.
- Confirm `.gitignore` covers them.
- Build, then grep the output bundle for known secret values. `EXPO_PUBLIC_*` is inside the bundle by design — confirm nothing in there is actually secret.

Report anything found before continuing. Do not fix a committed secret by deleting the file: it stays in history, and the key has to be rotated.

## Physical device

A simulator build proves nothing about fonts, shadows, permissions, or push. Confirm a preview build ran on a real device before submission, and say so if it did not.

## Report

Per step: passed, failed with output, or skipped by request. Then point at `/mobilekit:build 34` for what to watch once users are in it — after the release, not before.
