# mobilekit

Cross-agent entry point. Claude Code loads `SKILL.md`; Codex, Antigravity, Cursor, Zed and anything else following the `AGENTS.md` convention land here.

## If you are using mobilekit to build an app

**Read [`SKILL.md`](./SKILL.md) now.** It holds the operating rules, the state model, and the procedure for executing a prompt. Everything below is a map, not a substitute.

The library is `prompts/`, organized by phase. Its index and the reference build order are in [`prompts/README.md`](./prompts/README.md), and [`prompts/RULES.md`](./prompts/RULES.md) is read before every single prompt.

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

Commands live in `commands/`. Each is one phase. How they are invoked depends on the agent — see [`README.md`](./README.md) for the wiring per tool. Without slash commands, run a command file's content directly; they are plain Markdown with no host-specific syntax in the body.

Three things that hold regardless of which agent you are:

1. **`docs/PRODUCT.md` gates everything.** It does not exist → run discovery. Never infer the product from the folder name or an existing scaffold.
2. **Verify the installed version before writing setup code.** Read `package.json`, then that version's docs. Config layout moved in Tailwind 3→4, NativeWind 4→5, Reanimated 3→4, Sentry 7→8.
3. **Secrets stay server-side.** `EXPO_PUBLIC_*` ships inside the bundle and is public by definition.

## If you are working on mobilekit itself

This repo is the skill, not an app built with it.

- `SKILL.md` is the single source of truth for behavior. This file points at it; do not copy rules into here, they will drift.
- **File numbers in `prompts/` are stable IDs.** `05b-domain-model.md` keeps that name wherever it moves. `BUILD-PLAN.md` entries and the ~110 prose cross-references between prompts depend on them. Never renumber.
- Folder numbers (`1-discovery`) are phase order and may be reorganized; only `prompts/README.md` carries real links to fix.
- A new prompt goes in the folder matching its phase, with a unique number, and gets a row in `prompts/README.md`.
