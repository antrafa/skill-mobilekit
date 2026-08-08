# mobilekit — prompt library

Reusable prompts for building production-quality React Native apps with Expo, organized by phase. Drive them with the `/mobilekit:*` commands, or paste one by hand.

Folders are the phase order. File numbers are stable IDs — they never change, so `BUILD-PLAN.md` and cross-references between prompts keep working when a file moves.

---

## How to use

1. Read [**RULES.md**](./RULES.md) once yourself. It is short, and every prompt starts by reading it. It exists because the common failure is not bad code — it is an assistant deciding something you never chose.
2. Run [`1-discovery/00-product-discovery.md`](./1-discovery/00-product-discovery.md) first. It writes `docs/PRODUCT.md`, which every other prompt reads instead of guessing what you are building.
3. Create `AGENTS.md` from `PRODUCT.md` with [`1-discovery/00-agents-md-guide.md`](./1-discovery/00-agents-md-guide.md).
4. Decide screens and navigation with [`2-design/00c-design-conception.md`](./2-design/00c-design-conception.md) → `docs/DESIGN.md`. Screens built before this get rewritten.
5. Define the domain with [`3-foundation/05b-domain-model.md`](./3-foundation/05b-domain-model.md) → `docs/DOMAIN.md`.
6. Then follow the build order below, or pick individual prompts for an existing project.

Outputs live in the project's `docs/` — `PRODUCT.md`, `DESIGN.md`, `DOMAIN.md`, `BUILD-PLAN.md`. The library lives here. They are deliberately separate: the first four are documentation someone reads without knowing this skill exists.

Where a prompt offers a menu ("Option A / B / C"), that is a question for you, not a choice for the assistant to make silently.

---

## Index

### `1-discovery` — what are we building
| # | Prompt | Description |
|---|--------|-------------|
| — | [Rules](./RULES.md) | Read before every prompt: verify versions, don't invent, ask instead of assume |
| 00 | [Product Discovery](./1-discovery/00-product-discovery.md) | **Start here.** Interview that defines the product → `docs/PRODUCT.md` |
| 00 | [AGENTS.md Guide](./1-discovery/00-agents-md-guide.md) | Build a project-specific AGENTS.md from `PRODUCT.md` |

### `2-design` — what does it look like
| # | Prompt | Description |
|---|--------|-------------|
| 00c | [Design Conception](./2-design/00c-design-conception.md) | Screen inventory, navigation shape, per-screen states → `docs/DESIGN.md` |
| 03 | [Design System](./2-design/03-design-system.md) | Color, type, spacing, radius, elevation — centralized as tokens |

### `3-foundation` — the base everything sits on
| # | Prompt | Description |
|---|--------|-------------|
| 01 | [Expo Project Setup](./3-foundation/01-expo-project-setup.md) | Initialize Expo with TypeScript and Router |
| 02 | [NativeWind Setup](./3-foundation/02-nativewind-setup.md) | Install and configure NativeWind (Tailwind CSS) |
| 05b | [Domain Model & Data Layer](./3-foundation/05b-domain-model.md) | Entities, schema or existing-table mapping, types, fixtures |
| 24 | [Common UI Components](./3-foundation/24-common-ui-components.md) | Only the shared set `DESIGN.md` identified — nothing speculative |

### `4-platform` — auth, data, and the server side
| # | Prompt | Description |
|---|--------|-------------|
| 04 | [Auth with Clerk](./4-platform/04-authentication-clerk.md) | Managed authentication |
| 05 | [Auth with Database](./4-platform/05-authentication-database.md) | Custom auth with your own backend or Supabase |
| 06 | [Supabase Setup](./4-platform/06-supabase-setup.md) | Database, auth, and storage |
| 07 | [Zustand Setup](./4-platform/07-zustand-setup.md) | Global state with persistence |
| 12 | [React Query](./4-platform/12-react-query.md) | Data fetching with TanStack Query |
| 27 | [Secure Backend Integration](./4-platform/27-secure-backend-integration.md) | API routes, token generation, keeping secrets out of the bundle |

### `5-screens` — the app itself
| # | Prompt | Description |
|---|--------|-------------|
| 15 | [Onboarding Screen](./5-screens/15-onboarding-screen.md) | Welcome / intro experience |
| 16 | [Tab Navigation](./5-screens/16-tab-navigation.md) | Custom bottom tab bar |
| 17 | [Home Screen](./5-screens/17-home-screen.md) | Main dashboard / feed |
| 18 | [Detail Screen](./5-screens/18-detail-screen.md) | Item detail view |
| 19 | [Profile Screen](./5-screens/19-profile-screen.md) | User profile and account |
| 20 | [Settings Screen](./5-screens/20-settings-screen.md) | App preferences and configuration |
| 21 | [Form Screens](./5-screens/21-form-screens.md) | Create / edit forms |
| 22 | [List Screen](./5-screens/22-list-screen.md) | Lists with search and filtering |
| 23 | [Modals & Bottom Sheets](./5-screens/23-modal-bottom-sheet.md) | Reusable modals and sheets |

### `6-features` — capabilities, only if `PRODUCT.md` marks them "now"
| # | Prompt | Description |
|---|--------|-------------|
| 10 | [Push Notifications](./6-features/10-push-notifications.md) | Expo Notifications setup |
| 11 | [Reanimated Animations](./6-features/11-reanimated-animations.md) | Smooth, performant animations |
| 13 | [RevenueCat Purchases](./6-features/13-revenuecat-purchases.md) | In-app purchases and subscriptions |
| 14 | [Payment Gateway](./6-features/14-payment-gateway.md) | Stripe integration for payments |
| 25 | [Dark Mode](./6-features/25-dark-mode.md) | Light/dark theme support |
| 28 | [AI / LLM Features](./6-features/28-ai-features.md) | Text, streaming, and realtime voice/video — via your own server |
| 29 | [Internationalization](./6-features/29-internationalization.md) | Multiple languages, locale formatting, RTL |
| 31 | [Offline Support](./6-features/31-offline-support.md) | Cached reads, queued writes, honest degradation |
| 32 | [Deep Linking](./6-features/32-deep-linking.md) | Custom schemes, universal links, protected destinations |

### `7-ship` — the release gate
| # | Prompt | Description |
|---|--------|-------------|
| 30 | [Testing](./7-ship/30-testing.md) | Risk-driven test scope, from domain logic to one E2E path |
| 33 | [Accessibility Audit](./7-ship/33-accessibility-audit.md) | Cross-app sweep before first submission |
| 26 | [EAS Build & Deploy](./7-ship/26-eas-build-deploy.md) | Build, environment variables, store submission, OTA updates |

### `8-observability` — knowing what happens after
| # | Prompt | Description |
|---|--------|-------------|
| 08 | [PostHog Analytics](./8-observability/08-posthog-analytics.md) | Event tracking, feature flags, and A/B testing |
| 09 | [Sentry Error Tracking](./8-observability/09-sentry-error-tracking.md) | Error tracking and performance monitoring |
| 34 | [Post-Release Observability](./8-observability/34-post-release-observability.md) | The four numbers you watch once real users are in it |

---

## Suggested build order (new project)

```
00  → Product discovery → docs/PRODUCT.md   (nothing runs before this)
00  → Create AGENTS.md from PRODUCT.md
00c → Design conception → docs/DESIGN.md    (before any screen)
01  → Set up Expo project
02  → Install NativeWind
03  → Define design system
05b → Define the domain model             (before any screen)
24  → Build common UI components          (only the shared list from DESIGN.md)
15  → Build onboarding screen
04/05 → Set up authentication             (skip if PRODUCT.md says no accounts)
06  → Set up backend                      (if Supabase)
07  → Set up Zustand
12  → Set up React Query                   (if data comes from a remote source)
16  → Build tab navigation
17  → Build home screen
22  → Build list screen
18  → Build detail screen
21  → Build form screens                   (if users create data)
23  → Modals & bottom sheets
19  → Build profile screen
20  → Build settings screen
11  → Add animations
25  → Add dark mode
29  → Add i18n                             (if multiple languages)
27  → Secure backend integration           (before any service with a secret)
28  → Add AI features                      (if AI is in scope)
13/14 → Add purchases or payments          (only if PRODUCT.md marks it "now")
08  → Add analytics
09  → Add error tracking
10  → Add push notifications
32  → Deep linking                          (needed by 10, 14, and OAuth)
31  → Offline support                       (if required)
30  → Testing                               (earlier if the app handles money or auth)
33  → Accessibility audit                   (before first submission)
26  → Build and deploy
34  → Post-release observability            (after real users, not before)
```

`/mobilekit:plan` generates this list cut down to only the steps your `PRODUCT.md` and `DESIGN.md` justify. Skip every step whose capability is marked "later" or "never".

---

## Customization

- **Replace placeholders**: `[bracketed text]` is yours to fill — or let `PRODUCT.md` answer it
- **Never let the assistant guess the domain**: a decision marked `UNDECIDED` gets asked, not invented
- **Attach designs**: where a prompt says "attach design", provide the Figma export or screenshot
- **Skip what you don't need**: not every app needs payments or push notifications
- **Extend**: add your own prompts to the folder that fits; keep the number prefix unique
- **Keep AGENTS.md updated** as the stack changes

---

## Stack covered

Expo · React Native · TypeScript · Expo Router · NativeWind · Zustand + AsyncStorage · Clerk / Supabase / custom auth · Supabase · TanStack Query · PostHog · Sentry · Expo Notifications · Reanimated · RevenueCat · Stripe · Expo API Routes for anything holding a secret · provider-agnostic AI, always proxied server-side · EAS Build + EAS Update.

Cross-cutting concerns with their own prompts: i18n, offline, deep linking, testing, accessibility, post-release observability.
