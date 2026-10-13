<div align="center">

# Coachfolio — Open-Source Fitness Coaching Platform

**Free, self-hostable software for personal trainers and online fitness coaches.**
Build workout programs, deliver them to clients in a branded mobile app, track progress, and get paid. Your brand, your Stripe account, your data.

*An open-source alternative to Trainerize, TrueCoach, Everfit and My PT Hub.*

![Status](https://img.shields.io/badge/status-MVP%20in%20development-orange)
![License](https://img.shields.io/badge/license-MIT-blue)
![Next.js](https://img.shields.io/badge/Next.js-TypeScript-black)
![Supabase](https://img.shields.io/badge/Supabase-Postgres-3ECF8E)
![PWA](https://img.shields.io/badge/PWA-iOS%20%7C%20Android%20%7C%20Desktop-5A0FC8)

[Features](#features) · [Roadmap](ROADMAP.md) · [Quick start](#quick-start) · [Tech stack](#tech-stack) · [FAQ](#faq) · [**Hire me for a custom build**](#hire-me-custom-fitness-app-development)

</div>

---

## What is Coachfolio?

Coachfolio is an **open-source personal trainer app and online coaching platform**. Coaches use it to create **workout programs**, assign them to clients, and follow their progress. Clients get a **mobile workout app** (an installable PWA for iPhone, Android and desktop) with guided workouts, timers, demo videos and progress tracking.

It is built for:

- **Personal trainers** moving clients from PDFs, spreadsheets and WhatsApp to a real app
- **Online fitness coaches** who want a **white-label fitness app** without paying per client
- **Gyms, studios, kickboxing / martial arts / yoga / CrossFit coaches** who need programs and member access
- **Developers and agencies** who want a solid **Next.js + Supabase fitness app template** to build on

## Why another coaching app?

Commercial coaching platforms work, but coaches often complain about:

| Common pain point | Coachfolio approach |
|---|---|
| Price rises with every client tier | **Unlimited clients.** Self-host for free, or use flat hosted pricing |
| Branded app costs extra | **White-label by default:** your logo, colours and domain |
| Platform takes a cut of client payments | **Your own Stripe account** (Stripe Connect), no platform surcharge |
| Hard to leave, with limited data export | **You own the data.** Full export, open database schema |
| Closed product, can't add features | **Open source (MIT).** Extend it yourself or [hire me](#hire-me-custom-fitness-app-development) |

## Features

> 🚧 **Status: MVP in development.** ✅ = shipped, ⏳ = in progress / planned. See the full [ROADMAP.md](ROADMAP.md).

### For coaches
- ⏳ Coach workspace with your own branding (logo, colours, name)
- ⏳ Exercise library with demo videos and instructions
- ⏳ Workout builder: warm-up, blocks, sets/reps, rounds, work/rest intervals, cool-down
- ⏳ Program builder: multi-week programs with ordered sessions
- ⏳ Invite clients and control access (grant, expire, revoke)
- ⏳ Client list with adherence and last-workout overview
- ⏳ Subscriptions and one-off payments via Stripe Connect
- ⏳ Data export (CSV/JSON)

### For clients (members)
- ⏳ Installable mobile app (PWA) for iPhone, Android and desktop
- ⏳ Home dashboard: next workout, weekly goal, streak
- ⏳ Guided workout player with interval timer, video and captions
- ⏳ Resume a workout on any device, with duplicate-safe completion
- ⏳ Progress: completed sessions, training minutes, history
- ⏳ Profile, goals, equipment, time zone, data export and deletion requests

### Planned (phase 2+)
Coach–client chat · check-in forms · body measurements and progress photos · nutrition and meal plans · automated program delivery · push notifications · class booking · custom domains · multi-coach teams · wearables (Apple Health, Google Fit) · native iOS/Android apps · AI program assistant · program marketplace. See the [ROADMAP](ROADMAP.md).

## Screenshots

> Screenshots and a live demo will be added as the MVP ships.

<!-- ![Coachfolio workout player – open source fitness app](docs/screenshots/workout-player.png) -->

## Tech stack

| Layer | Technology |
|---|---|
| Frontend | Next.js (App Router), React, TypeScript, Tailwind CSS |
| Backend | Next.js route handlers / server actions |
| Database and auth | Supabase (Postgres, Auth, Row-Level Security) |
| Payments | Stripe Billing and Stripe Connect |
| Video | Cloudflare Stream (signed playback); pluggable |
| Email | Any SMTP / transactional email provider |
| Hosting | Vercel, or self-host with Docker |
| Mobile | Progressive Web App; Capacitor native wrapper planned |

**Architecture principles:** multi-tenant from day one (`coach_id` on every row), Row-Level Security for client privacy, immutable workout versions so history never changes, idempotent workout completion, and server-side secrets only.

## Quick start

> Setup scripts land with the first MVP release. Planned flow:

```bash
git clone https://github.com/kapoordeepanshu/coachfolio.git
cd coachfolio
cp .env.example .env.local     # add Supabase, Stripe and video keys
pnpm install
pnpm db:migrate && pnpm db:seed
pnpm dev                        # http://localhost:3000
```

## Hire me: custom fitness app development

I build and maintain Coachfolio, and I take on **custom fitness app projects** built on it. That's usually much faster and cheaper than starting from zero.

**What I can build for you:**
- 🏋️ **Your branded coaching app**: your logo, domain and content, deployed on accounts you own
- 🧩 **Custom features**: anything on the [roadmap](ROADMAP.md) or specific to your business (nutrition, booking, challenges, gym check-in, wearables…)
- 💳 **Payments and memberships**: Stripe subscriptions, trials, coupons, one-off programs
- 📱 **App Store / Google Play apps** from the same codebase
- 🔁 **Migration** from Trainerize, TrueCoach, Everfit, spreadsheets or PDFs
- 🛠️ **Hosting, maintenance and support**

**How it works:** your custom work lives in **your own private repository** under your account. You own your custom code and content, and the open-source core stays MIT-licensed.

📩 **Contact:** [LinkedIn – Deepanshu Kapoor](https://www.linkedin.com/in/deepanshukapoor/) · [Portfolio](https://kapoordeepanshu.github.io/) · [Open an issue](https://github.com/kapoordeepanshu/coachfolio/issues/new?title=Custom%20build%20request)

## FAQ

**Is Coachfolio free?**
Yes. The core is open source under the MIT license. Self-host it for free with unlimited coaches and clients.

**Is it an alternative to Trainerize or TrueCoach?**
It covers the same core workflow: programs, a client workout app, progress tracking and payments. It's open source, self-hostable and white-label. It's newer and still growing; see the [roadmap](ROADMAP.md).

**Does it work on iPhone and Android?**
Yes, as an installable Progressive Web App. Native App Store / Google Play builds are planned.

**Can I use it for my gym, studio or kickboxing/yoga/CrossFit classes?**
Yes. Programs and workouts are fully configurable. Multi-coach teams are on the roadmap.

**Can you add a feature I need?**
Yes. Open an issue, or [hire me](#hire-me-custom-fitness-app-development) to build it.

**Is client data private?**
Each coach's data is isolated with Postgres Row-Level Security, and clients can only see their own records. When you self-host, the data stays on your infrastructure.

## Contributing

Contributions are welcome: issues, feature ideas, translations, exercise data and pull requests. Please open an issue first for larger changes.

## License

[MIT](LICENSE). Free for personal and commercial use.

---

<sub>Keywords: open source fitness app, personal trainer app, online coaching platform, fitness coaching software, workout builder, workout planner, workout tracker, gym management software, white label fitness app, Trainerize alternative, TrueCoach alternative, Everfit alternative, Next.js fitness app, Supabase fitness app, PWA workout app, self-hosted fitness app.</sub>
