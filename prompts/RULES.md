# Prompt Rules

Read this before every prompt in this collection. It exists because the common failure is not bad code — it is an assistant deciding something the developer never chose, or applying setup steps from a version that no longer exists.

## 1. PRODUCT.md is the source of truth

- Read `docs/PRODUCT.md` (from `00-product-discovery.md`), `docs/DESIGN.md` (from `00c-design-conception.md`) and `docs/DOMAIN.md` (from `05b-domain-model.md`) before any task.
- Screen prompts read `DESIGN.md` for the screen's empty / loading / error states. A screen shipped without them is not done.
- Use the domain vocabulary recorded there. Never `Item`, `Data`, `Record`, `Thing`.
- If a prompt needs a decision `PRODUCT.md` marks `UNDECIDED`, **ask, then update `PRODUCT.md`**. Do not decide it inline and move on.
- If a capability is marked "later" or "never", do not build it and do not install its dependency.

## 2. Verify the installed version before writing setup code

- Check `package.json` for the installed version, then read the official docs **for that version** (via context7 or the linked URL).
- Do not apply setup steps from memory, from a blog post, or from a snippet in this collection. Config layout changes between majors — Tailwind 3→4, NativeWind 4→5, Reanimated 3→4, Sentry 7→8 all moved or deleted required files.
- If the installed version's docs contradict a step in a prompt, follow the docs and say so.

## 3. Inspect the repo before creating files

- Paths in these prompts are illustrative. Check whether this project uses `app/` or `src/app/`, whether `tailwind.config.js` or `babel.config.js` exist at all, and follow what is already there.
- Never create a config file just because a prompt mentions it. Create it only if the installed version requires it.

## 4. Options are questions

- Where a prompt lists patterns (Option A / B / C), present them and ask. Do not pick silently.
- Recommend one, in one line, with the reason.

## 5. Do not invent

- No field, table, endpoint, event name, or user-facing copy that is not in `PRODUCT.md`, `DOMAIN.md`, an inspected schema, or a real contract.
- Ask before adding any dependency. Say what it replaces and why doing it by hand is worse.

## 6. Secrets

- Secrets stay server-side (API route or backend). `EXPO_PUBLIC_*` ships inside the bundle and is public by definition.
- Never commit keys, service-account files, or `.env`.

## 7. Report honestly

- State what you skipped, what you assumed, and what you could not verify.
- If a step failed, show the output. Do not report done on partial work.
