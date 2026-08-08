# Changelog

All notable changes to this project are documented here. The format follows
[Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and this project adheres to
[Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [2.0.0] — 2026-08-08

A structural release. The workflow engine moved into the skill so the whole thing works
when installed by a skills registry, prompt filenames became the ids, and 13 prompts
closed gaps that could block a store submission.

### Breaking

- **Prompt filenames replace numeric prefixes.** `05b-domain-model.md` is now
  `domain-model.md`, `27-secure-backend-integration.md` is `secure-backend.md`, and so on
  for all 38 existing prompts. The numbering had already collided — two `00`s, a `00c`
  with no `00a`, and a `05` and `05b` in different phases — and it never ordered anything,
  since the order lives in `prompts/README.md` and in `BUILD-PLAN.md`. An existing
  `docs/BUILD-PLAN.md` referring to numbers must be regenerated with the `plan` phase.
- **`init` no longer copies the prompt library into the project.** Prompts are read from
  the installed skill, so a fix reaches every project at once. A project that needs its own
  rules writes `docs/mobilekit-overrides.md`, read after `prompts/RULES.md` and winning on
  conflict. An existing `mobilekit/` directory in a project can be deleted.
- **The workflow engine moved from `commands/` to `workflow/`.** Slash commands are now
  three-line aliases. This was a correctness fix: skills registries install `SKILL.md` and
  its directory but not a host's command directory, so the `BUILD-PLAN` format, the secret
  leak sweep and the `status` drift check were unreachable for anyone who installed the
  skill rather than cloning it.
- **`prompts/RULES.md` is the single source of truth for prompt behaviour.** The three
  rules previously duplicated across `SKILL.md`, `AGENTS.md` and `README.md` now live in
  one place and are pointed at.

### Added

- **`native-permissions.md`** — every OS permission the app asks for, with all three
  denial paths including permanently-denied and its route to the settings screen. It was
  previously improvised inline by three separate prompts.
- **`media-upload.md`** — camera and library capture, compression, EXIF handling, signed
  uploads, the pending state in the domain, and orphan cleanup. Discovery had asked about
  media since the first version and no prompt answered.
- **`content-moderation.md`** — report, block, review queue and the developer contact
  route. An app with user-generated content and none of these is rejected by store review.
- **`store-compliance.md`** — privacy manifest and required-reason APIs, data-safety
  declarations, tracking permission, policy URL, reviewer account, age rating, listing
  assets. `eas-build.md` produced a binary; this is what decides whether it is accepted.
- **`privacy-consent.md`** — GDPR/LGPD consent, deferred SDK initialization, withdrawal
  that actually stops collection. Ordered **before** `analytics.md`: an SDK that collects
  on launch has already collected before any consent screen appears.
- **`api-integration.md`** — an API you do not own, across OpenAPI, undocumented REST and
  GraphQL, with the auth, pagination, error-taxonomy and environment questions.
- **`account-recovery.md`** — password reset, credential and email changes. Both auth
  prompts assumed these screens existed and neither built them.
- **`biometric-lock.md`** — Face ID and fingerprint as a local gate over an existing
  session, with the mandatory fallback and the enrollment-changed case.
- **`performance.md`** — startup, lists, images, re-renders and bundle, measured on a
  low-end device before and after each fix.
- **`ci-cd.md`** — what runs per pull request, per merge and per release tag, and where
  store credentials live.
- **`release-rollback.md`** — the levers when a release goes bad, ordered by reach, and
  prepared before they are needed rather than improvised during an incident.
- **`sdk-upgrade.md`** — one major at a time, verified between each.
- **`legacy-modernization.md`** — a second entry point, for an app that already ships.
  Inventory replaces the interview, across four starting points: bare React Native behind,
  Expo behind, hybrid Cordova/Ionic/WebView, and native Swift/Kotlin adopting React Native
  incrementally.
- **`docs/COMMANDS.md`** — a reference for every command: what it reads, what it refuses,
  what it produces.
- `CONTRIBUTING.md`, `CHANGELOG.md`, `LICENSE`.

### Changed

- **Every prompt grills one question at a time.** `### Ask first` is now `### Grill`, and
  `prompts/RULES.md` §1 makes the conduct binding: one question per message with a
  recommended answer, facts looked up rather than asked, decisions put to the developer.
  Previously only discovery and design carried that rule and the other 31 prompts listed
  their questions, which an agent reads as permission to ask all of them at once.
- **Documentation is requested rather than assumed.** `prompts/RULES.md` §3 replaces the
  ten references to a specific documentation MCP server with a cascade: read the installed
  version, use a docs tool if the agent has one, otherwise ask the developer — with
  `docs/vendor/<lib>@<version>.md` as the place an answer is kept so the ask happens once.
  Proceeding from memory is allowed only with the unverified steps named in the report.
- `ship` now includes the performance pass, the consent check, store compliance and the
  Expo project doctor.
- `install.sh` reads the skill name from `SKILL.md` frontmatter instead of the directory
  name, so cloning the repo under its GitHub name still produces `/mobilekit:*`. It also
  links Antigravity and Cursor.
- `SKILL.md` frontmatter carries `license` and `metadata.version`.

### Removed

- `agents/openai.yaml` — three lines, referenced by nothing.

## [1.0.0]

Initial release: 38 prompts across eight phases, eight slash commands, `install.sh` for
Claude Code and Codex.
