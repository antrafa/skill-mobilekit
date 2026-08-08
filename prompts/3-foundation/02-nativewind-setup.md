# NativeWind Setup

Install and configure NativeWind (Tailwind for React Native).

---

## Prompt

Read `mobilekit/RULES.md` and AGENTS.md first.

Set up NativeWind in this Expo app.

### Before you write anything

**The setup differs substantially between versions, and stale steps are the single most common failure here.** Check `package.json` for the installed `nativewind` and `tailwindcss` versions, then follow the official installation guide **for those exact majors** (context7, or https://www.nativewind.dev). Specifically:

- Whether a `tailwind.config.js` is required at all, or the theme is defined in CSS
- Which Tailwind directives or `@import` lines the CSS entry file needs
- Whether a Babel plugin/preset is required, or the Metro transformer handles it alone
- Where the CSS entry file must be imported

Do not create `tailwind.config.js` or `babel.config.js` because an older guide mentions them. Create a config file only if the installed version requires it. If the repo already has these files, follow what is there.

### Build

1. Install NativeWind and its peer dependencies at versions compatible with the installed Expo SDK.
2. Apply the config the installed version's docs specify: CSS entry, Metro config, Babel (only if required), TypeScript declarations.
3. Import the CSS entry in the root layout.
4. Set content/source paths so every route and component file is scanned.

### Done when

- [ ] A throwaway component styled only with `className` renders correctly on a device — not just in web
- [ ] `className` type-checks in `.tsx` files with no editor error
- [ ] No existing screen was modified
- [ ] You state which version's setup you followed, and any step in this prompt that no longer applied

Leave the design tokens to `03-design-system.md` — this prompt only makes styling work.
