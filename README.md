# Hackathon Kit

A production-ready, full-featured hackathon website template built with Vue 3, TypeScript, Tailwind CSS, and Supabase. Fork it, configure it, deploy it — have a working hackathon site in minutes.

## Features

- Beautiful responsive landing page with countdown timer, typewriter effects, and scroll animations
- Team registration and management (create, join, leave, invite, lock)
- User authentication (email/password with Supabase Auth)
- Real-time team updates via Supabase Realtime subscriptions
- Admin dashboard with stats, charts, user management, and announcement system
- Check-in system with QR codes
- Project submission and review
- Redeem code distribution (for sponsor API credits)
- Export data as JSON, CSV, or PDF
- i18n support (English + Chinese included, easily extensible)
- Dark/light theme toggle
- RSVP confirmation system
- Team invitation system with email notifications (Supabase Edge Functions)

## Quick Start

1. **Fork this repository**

2. **Set up Supabase**
   - Create a new project at [supabase.com](https://supabase.com)
   - Run the SQL migrations in `supabase/migrations/` and `docs/supabase-setup.md`
   - Copy your project URL and anon key

3. **Configure**
   ```bash
   cp .env.example .env
   # Edit .env with your Supabase credentials
   ```

4. **Customize content**
   - Edit `src/i18n/en.ts` and `src/i18n/zh.ts` — replace all `[PLACEHOLDER]` values
   - Replace `[EVENT]` in `src/components/sections/HeroSection.vue`
   - Add sponsor logos to `public/sponsors/`
   - Add venue/event photos to `public/photos/`
   - Update `index.html` title and meta description

5. **Install and run**
   ```bash
   npm install
   npm run dev
   ```

6. **Deploy**
   ```bash
   npm run build
   # Deploy the dist/ directory to GitHub Pages, Vercel, Netlify, etc.
   ```

## Configuration Guide

See `config/event.example.yaml` for a complete reference of all configurable values.

### Key files to edit:

| File | What to change |
|------|---------------|
| `.env` | Supabase URL and anon key, site URL |
| `src/i18n/en.ts` | All English text content |
| `src/i18n/zh.ts` | All Chinese text content |
| `src/components/sections/HeroSection.vue` | Event name, countdown dates, sponsor logos |
| `src/components/sections/SponsorsSection.vue` | Sponsor logos and links |
| `src/components/sections/TechSection.vue` | Sponsor logos |
| `src/components/sections/PrizesSection.vue` | Award configuration |
| `src/pages/VisionPage.vue` | Event vision/about content |
| `src/pages/RulesPage.vue` | Official rules |
| `src/components/layout/AppHeader.vue` | Logo |
| `src/components/layout/AppFooter.vue` | Footer links |
| `index.html` | Page title, meta description |

## Supabase Setup

See [docs/supabase-setup.md](docs/supabase-setup.md) for complete SQL to create all required tables.

### Required tables:
- `profiles` — user profiles
- `teams` — team data
- `submissions` — project submissions
- `announcements` — live announcement banner
- `redeem_codes` — sponsor API credit codes
- `admin_config` — admin password hash and settings
- `team_invitations` — invitation system

## Deployment

See [docs/deployment.md](docs/deployment.md) for step-by-step deployment guides.

### GitHub Pages
```bash
npm run build
# Push dist/ to gh-pages branch
```

### Vercel
Connect your repo to Vercel. It auto-detects Vite and deploys.

### Any static host
The `dist/` directory is a static site. Deploy it anywhere that serves static files.

## Tech Stack

- **Vue 3** + Composition API
- **TypeScript**
- **Vite 8**
- **Tailwind CSS 4**
- **Supabase** (Auth, Database, Realtime, Edge Functions)
- **QRCode** generation
- **jsPDF** for PDF exports
- **canvas-confetti** for celebrations

## License

MIT
