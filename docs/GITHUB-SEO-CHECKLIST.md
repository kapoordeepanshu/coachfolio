# GitHub SEO and lead checklist

These are the things that get the repo found on Google and GitHub search and turn visitors into clients.

## Repo settings (do these on day one)
- **Repo name:** `coachfolio` (keywords carried by the description, which Google shows in the result title)
- **About / description** (GitHub's ~350-character field; Google uses it as the snippet):
  > Open-source fitness coaching platform & personal trainer app. Workout builder, client PWA, progress tracking, Stripe payments. Self-hosted alternative to Trainerize & TrueCoach. Next.js + Supabase.
- **Website:** link to the live demo
- **Topics** (up to 20): `fitness-app` `personal-trainer` `fitness-coaching` `workout-tracker` `workout-planner` `gym-management` `online-coaching` `trainerize-alternative` `white-label` `saas` `pwa` `nextjs` `supabase` `typescript` `stripe` `self-hosted` `open-source` `fitness` `workout` `coaching-platform`
- **Social preview image** (Settings → General): 1280×640 with the logo, tagline and a screenshot
- Pin the repo on your GitHub profile; add a profile README that links to it and says "Available for hire"

## README
- H1 and first paragraph contain the main keywords (done)
- Real screenshots with descriptive alt text, plus a GIF of the workout player
- Live demo link with demo credentials
- "Hire me" section with **at least two** contact routes (done; fill in the placeholders)
- Keep the ✅/⏳ status honest. Overclaiming kills trust with buyers.

## Traffic sources (GitHub alone is slow)
- Submit to: AlternativeTo (as an alternative to Trainerize/TrueCoach/Everfit), awesome-selfhosted, awesome-nextjs, awesome-supabase, Product Hunt, Hacker News "Show HN", r/selfhosted, r/personaltraining, r/nextjs
- Write 3–5 blog posts on dev.to / Medium / your site, linking to the repo: "How I built an open-source Trainerize alternative with Next.js + Supabase", "Idempotent workout completion", "Multi-tenant RLS in Supabase"
- Use GitHub Releases with changelogs; each release is an indexable page and reaches watchers
- Fill GitHub Discussions with a "Need a custom build?" category
- Link the repo from your Upwork / LinkedIn / Fiverr portfolio

## Before the first public push
- [ ] `Fitness-App-MVP-Blueprint.md` (a client's job attachment) is excluded by `.gitignore`. Never commit it.
- [x] Contact links filled in README.md
- [ ] Check domain (coachfolio.app / .dev) and a trademark search before commercial launch
- [x] `LICENSE` (MIT) added
- [ ] No secrets in history (`git log -p | grep -i key` before pushing)
