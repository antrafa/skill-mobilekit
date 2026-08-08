# EAS Build & Deploy

Builds, store submission, and over-the-air updates.

---

## Prompt

Read `mobilekit/RULES.md`, `docs/PRODUCT.md` and AGENTS.md first.

Set up EAS Build for this app.

**Check the installed `eas-cli` version and follow the current docs** (https://docs.expo.dev/build/introduction/). Commands here move: environment-variable management in particular has been reorganized — use the current environment-variable commands rather than older secret commands, and confirm against `eas --help` for the installed version before scripting anything.

### Ask first

- Which platforms ship, and to which stores?
- Are the developer accounts and store listings in place? Missing accounts block submission, not building.
- Who owns the credentials — EAS-managed or manually supplied?
- Which environments are needed (development, preview, production), and does each point at a different backend? That decides how many sets of variables exist.
- Is over-the-air updating wanted? It only covers JS changes — a native dependency added later still needs a store build. Confirm the developer understands the boundary.

### Build

**Profiles** — a development profile producing a dev client, a preview profile for internal distribution, and a production profile with version auto-increment. Do not copy a profile block from memory; generate it with the CLI and then adjust.

**Environment variables** — this is where secrets leak:

- `EXPO_PUBLIC_*` variables are embedded in the bundle and readable by anyone with the app. Only genuinely public values (publishable keys, project URLs) belong there
- Server-side secrets belong to the API route or backend deployment, never to the app build
- Store per-environment values in EAS with the current environment-variable commands, and keep secret values out of the repo
- The Android submission credential is a **Google Play service-account JSON** — a different file from Firebase's `google-services.json`, and easily confused. Reference it by path, add it to `.gitignore`, and never commit it. Same for iOS keys

**Verification before the first store build**

- Confirm the bundle contains no secret: build, then search the output for known secret values
- Test a preview build on a physical device — not a simulator build — before submitting

**Submission and updates** — configure submission for the target stores, then set up update channels matched to build profiles so a preview update cannot reach production users. Update messages should say what changed.

### Done when

- [ ] A development build runs on a physical device
- [ ] A preview build installs and works against the correct environment
- [ ] Grepping the built bundle for secret values returns nothing
- [ ] No credential file is tracked by git — verified with `git ls-files`
- [ ] An OTA update reaches a build on the matching channel and not on others
- [ ] Version and build numbers increment correctly between production builds
