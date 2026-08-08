# mobilekit

A phase-driven workflow for building React Native / Expo apps with an AI coding agent — from "I have an idea" to "I know what broke in production".

38 prompts organized into eight phases, plus eight commands that decide **which** prompt runs next and refuse the ones whose prerequisites are missing. That refusal is the point: the prompts alone are a folder you read; the commands know where the project is.

```
1-discovery      what are we building        → docs/PRODUCT.md
2-design         screens, navigation, states → docs/DESIGN.md
3-foundation     Expo, NativeWind, domain model, shared components
4-platform       auth, database, state, data fetching, server-side secrets
5-screens        the app itself
6-features       push, payments, AI, i18n, offline, deep linking, dark mode
7-ship           testing, accessibility, EAS build & submit
8-observability  analytics, error tracking, what you watch after release
```

## The flow

| Command | Phase | Writes |
|---|---|---|
| `init` | install the library into a project + AGENTS.md | `mobilekit/` |
| `discovery` | product interview — never infers the domain | `docs/PRODUCT.md` |
| `design` | screen inventory, navigation shape, per-screen states | `docs/DESIGN.md` |
| `plan` | cuts 38 prompts down to only what this app needs | `docs/BUILD-PLAN.md` |
| `next` | runs the first unchecked step, one at a time | ticks the box |
| `build <topic>` | one prompt out of order — for existing projects | — |
| `ship` | release gate: testing → a11y → error tracking → EAS, plus a secret-leak sweep | — |
| `status` | where the project is, and where the plan disagrees with the repo | nothing |

The library and the documents it produces stay separate. `docs/PRODUCT.md` is read by people who do not know this tool exists.

## Install

```bash
git clone git@github.com:antrafa/skill-mobilekit.git ~/.agents/skills/mobilekit
~/.agents/skills/mobilekit/install.sh
```

`install.sh` is idempotent and only creates symlinks — it copies nothing and overwrites no config.

### What gets wired where

| Agent | Mechanism | Invocation |
|---|---|---|
| **Claude Code** | `~/.claude/skills/mobilekit` → repo · `~/.claude/commands/mobilekit` → `commands/` | `/mobilekit:next` |
| **Codex** | `~/.codex/prompts/mobilekit-*.md` → `commands/*.md` (Codex prompts are flat, hence the prefix) | `/mobilekit-next` |
| **Any AGENTS.md agent** | `AGENTS.md` at the repo root | point the agent at the repo, or run a `commands/*.md` file directly |

Antigravity, Cursor, Zed and anything else following the `AGENTS.md` convention read the root file. If your agent expects commands in a specific directory, pass it:

```bash
./install.sh --commands-dir ~/.config/<agent>/prompts --prefix mobilekit-
```

Command bodies are plain Markdown with no host-specific syntax — the frontmatter carries `description` and `argument-hint`, which every host either uses or ignores. An agent with no slash-command support runs the file's content as a prompt.

## Design decisions worth knowing

**File numbers are stable IDs.** `05b-domain-model.md` keeps that name wherever it sits. Around 110 cross-references between prompts are prose mentions of filenames, and `BUILD-PLAN.md` entries are numbers — renumbering breaks all of them at once. Folder numbers are just phase order and can be reorganized freely.

**Options are questions.** Where a prompt lists Option A / B / C, the agent presents them and recommends one. It does not choose your auth provider or your palette.

**`UNDECIDED` is a value.** Discovery records what you did not answer rather than filling it with a plausible guess, and later prompts stop on it instead of inventing.

**Nothing runs before `PRODUCT.md`.** A repo scaffolded from a tutorial tells an agent nothing about the product being built, and that is exactly when agents confidently invent a domain.

## Extending

Add a prompt to the folder matching its phase, give it a number nothing else uses, and add a row to `prompts/README.md`. Keep the shape: a header saying when it applies, a `## Prompt` section, and a `### Done when` checklist that can actually be tested.
