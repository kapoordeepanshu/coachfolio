# Coachfolio Roadmap

This is the plan from MVP to a full coaching platform. Each phase ships something usable, and the next phase starts only after real coaches have used the current one.

**Legend:** `[ ]` planned · `[~]` in progress · `[x]` shipped

---

## Phase 0: Foundation (week 1)

- [ ] Repo setup: Next.js (App Router) + TypeScript + Tailwind + pnpm, ESLint/Prettier, lockfile committed
- [ ] Supabase project: migrations folder, seed data, local dev via Supabase CLI
- [ ] CI: GitHub Actions for lint, typecheck, tests and preview deploys
- [ ] `.env.example`, MIT `LICENSE`, `CONTRIBUTING.md`, issue/PR templates
- [ ] Multi-tenant base: `coaches` table, with `coach_id` on every tenant row and RLS policies
- [ ] Live demo site with synthetic data, for SEO and sales

## Phase 1: MVP (weeks 2–8)

The goal is for one coach to run real paying clients on it end to end.

### Accounts and tenancy
- [ ] Email/password auth with verification and recovery; Google login
- [ ] Coach signup creates a workspace (name, slug, logo, brand colour)
- [ ] Member invite by link/email into a coach workspace
- [ ] Roles: `owner`, `coach`, `member`
- [ ] Member access control: `access_until`, revoke, and expired state ("Contact coach")

### Content (coach side)
- [ ] Exercise library: name, instructions, muscle groups, equipment, video, thumbnail
- [ ] Seed exercise library from Creative Commons data (wger dataset, with attribution)
- [ ] Workout builder: warm-up / blocks / cool-down, sets × reps, rounds, work/rest seconds
- [ ] Immutable workout versions (editing creates a new version and history keeps the old one)
- [ ] Program builder: weeks → ordered sessions; draft and published states
- [ ] Assign a program to a member, or let members choose from the coach's catalog
- [ ] CSV/JSON import for exercises and programs

### Member app (PWA)
- [ ] Installable PWA: manifest, icons, install instructions per device
- [ ] `/home`: next workout, Start/Resume, weekly goal, total sessions, coach message
- [ ] `/programs`: catalog and detail; enroll; switch with confirmation (history kept)
- [ ] `/workouts/[id]`: player with timestamp-based timer, Start/Pause/Reset, Prev/Next, video and captions, text fallback
- [ ] Save block position; resume across devices from server state
- [ ] Finish with an idempotent request ID (retries never double-count); "Not yet saved / Retry" state
- [ ] `/progress`: completed sessions, training minutes, weekly goal (member time zone, Monday-start week), history
- [ ] `/profile`: goal, weekly target, equipment, time zone, access status, privacy/terms, sign out

### Coach dashboard (minimal)
- [ ] Client list: active program, last workout, sessions this week
- [ ] Client detail: workout history

### Payments
- [ ] Stripe Connect onboarding per coach (money goes to the coach's own account)
- [ ] Coach creates plans (monthly subscription / one-off program purchase)
- [ ] Checkout → webhook → `member_access` sync (idempotent webhooks)
- [ ] Stripe customer portal for members (cancel, update card)

### Video
- [ ] Video provider adapter interface (Cloudflare Stream first)
- [ ] Signed, short-lived playback tokens only for members with access
- [ ] Upload from the coach dashboard; readiness and caption status

### Privacy, security and ops
- [ ] RLS tests: member A can never read member B or coach B data
- [ ] Rate limiting on auth, completion and token endpoints; CSRF/origin checks
- [ ] Data export (member and coach) and account deletion flow
- [ ] Privacy policy and terms templates (GDPR / Swiss FADP aware)
- [ ] Error monitoring, uptime check, daily backups and a documented restore

**MVP exit criteria:** 3–5 real coaches with paying clients, no cross-tenant data leaks, no double-counted workouts, and payments that grant and revoke access automatically.

## Phase 2: Retention and switching features (months 3–5)

These are the features that make coaches leave Trainerize, TrueCoach or Everfit.

- [ ] Coach ↔ client chat (realtime), with attachments
- [ ] Weekly check-in forms (custom questions, photos, coach reply)
- [ ] Body metrics: weight and measurements, with charts
- [ ] Progress photos (private storage, side-by-side compare)
- [ ] Exercise logging: actual sets, reps and weight; personal records
- [ ] Automation: drip programs, auto-assign on purchase, reminder emails
- [ ] Push notifications (web push; native later)
- [ ] Adherence dashboard: missed workouts and at-risk client alerts
- [ ] Custom domain per coach (`app.coachname.com`)
- [ ] Full white-label: app name, icons, splash, email sender
- [ ] Coupons, free trials, bundles, waitlists
- [ ] Program templates library (copy and customise)
- [ ] i18n: English plus a second language (e.g. German / Hindi / Spanish)
- [ ] One-click migration importers (CSV from Trainerize / TrueCoach / Everfit / spreadsheets)

## Phase 3: Platform (months 6–12)

- [ ] Nutrition: macro targets, food logging (Open Food Facts), meal plans, recipes
- [ ] Booking: 1:1 sessions, group classes, calendar sync (Google/Outlook)
- [ ] Multi-coach teams / gyms: roles, shared clients, revenue split
- [ ] Native iOS and Android apps (Capacitor) with App Store / Play Store builds
- [ ] Wearables: Apple Health, Google Health Connect, Garmin, Fitbit
- [ ] Challenges, leaderboards, badges and streaks
- [ ] Community feed / groups
- [ ] Offline workouts (downloaded sessions, sync queue)
- [ ] AI assistant: draft programs from a brief, summarise check-ins, suggest progressions
- [ ] Program marketplace: coaches sell programs to the public
- [ ] Public API and webhooks; Zapier / Make integrations
- [ ] Analytics: revenue, churn, LTV, retention cohorts

---

## Architecture decisions (fixed early)

| Decision | Why |
|---|---|
| Multi-tenant with `coach_id` + RLS from day one | Retrofitting tenancy later is a rewrite |
| Immutable `workout_versions` | Edits never corrupt client history |
| Idempotent completion and webhooks | Retries and flaky mobile networks never double-count |
| Provider adapters (video, email, payments) | Self-hosters can swap vendors |
| PWA first, native later | One codebase, no app-store review for the MVP |
| MIT core; custom client work in private repos | Maximum adoption; clients own their custom code |

## Core data model (MVP)

| Table | Key fields |
|---|---|
| `coaches` | id, name, slug, logo_url, brand_color, stripe_account_id |
| `memberships` | coach_id, user_id, role (owner/coach/member) |
| `profiles` | user_id, name, goal, equipment, weekly_target, timezone, accepted_terms_at |
| `exercises` | coach_id (null = global), name, instructions, muscles, equipment, video_asset_id |
| `workouts` / `workout_versions` | coach_id, version, title, planned_minutes, published_at |
| `workout_blocks` | workout_version_id, position, exercise_id, sets, reps, work_s, rest_s, rounds |
| `programs` / `program_sessions` | coach_id, title, level, weeks; week, position, workout_version_id |
| `enrollments` | user_id, program_id, status (active/archived/completed), one active per user per coach |
| `workout_sessions` | user_id, enrollment_id, workout_version_id, state, current_block, active_seconds, completion_request_id (unique) |
| `member_access` | coach_id, user_id, access_until, revoked_at, source (manual/stripe) |
| `plans` / `subscriptions` | coach_id, stripe_price_id; user_id, status, current_period_end |
| `video_assets` | coach_id, provider, provider_asset_id, ready, captions_ready |
| `audit_log` | actor, action, target, at |

## Business model

| Tier | Offer |
|---|---|
| **Self-hosted (free, MIT)** | Full core, unlimited clients |
| **Hosted Starter** | Hosted for you, Coachfolio branding, small client cap |
| **Hosted Pro** | White-label, custom domain, payments, chat; flat price, unlimited clients |
| **Gym / Team** | Multi-coach, roles, analytics |
| **Custom development** | Branded builds, custom features, native apps, migrations ([hire me](README.md#hire-me-custom-fitness-app-development)) |

## Custom client builds: how they're delivered

- Each client gets their **own private repository** (a fork or template copy), not a branch in this public repo. That keeps their code, branding and secrets private.
- Generic improvements made for clients are contributed back to the open-source core, only when the contract allows it.
- Contract template: client owns their custom code and content; the core stays MIT; pre-existing Coachfolio code is licensed, not assigned.
