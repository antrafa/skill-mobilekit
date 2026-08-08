# PostHog Analytics

Event tracking, feature flags, A/B tests. Skip if `PRODUCT.md` marks analytics "later" or "never".

Prereq: a PostHog project and API key.

---

## Prompt

Read `mobilekit/RULES.md`, `docs/PRODUCT.md` and AGENTS.md first.

Add PostHog to this app.

**Check the installed `posthog-react-native` version and follow its docs** (context7, or https://posthog.com/docs/libraries/react-native). Whether the provider takes an API key directly or a pre-constructed client, and how autocapture is configured, differ across versions — do not paste initialization from memory.

### Ask first — what is worth measuring?

An event list copied from a template produces dashboards nobody reads. Derive it instead:

- What is the **success action** in `PRODUCT.md`? That is the one event that must exist.
- What are the 2–3 steps immediately before it? Those are the funnel.
- Which drop-off do you actually suspect? Instrument that, and add an abandonment event where the user leaves before succeeding.
- Feature flags and A/B tests: is there a real decision waiting on data, or is this speculative? If speculative, skip — an unused flag is dead code with a remote kill switch.

Present the proposed event list with properties and get approval. Cap it: **5–8 events to start.**

### Build

- Install and initialize once; key via `EXPO_PUBLIC_POSTHOG_API_KEY`, host via env if self-hosted
- Wrap the app with the provider in the root layout, and never re-initialize elsewhere
- Identify the user after authentication resolves, using the auth provider's stable user id. Set changing traits on identify; set immutable ones (signup date) once
- Reset on sign-out, or the next user on that device inherits the previous identity
- Capture the approved events at the moments named in the list. `snake_case`, past tense, consistent property names across events
- Duration metrics: capture the start timestamp in a ref on mount so the value is real rather than re-rendered
- **No PII in properties.** No email, no free-text user input, no auth tokens
- Screen-view tracking: prefer the library's automatic navigation integration over a manual call per screen

### Done when

- [ ] Events appear in PostHog from a device, with the expected properties
- [ ] The success-action funnel is visible end to end
- [ ] Identify fires once after auth; sign-out resets
- [ ] No UI changed, no PII sent, no keys hard-coded
- [ ] Event list documented so the next event follows the same naming
