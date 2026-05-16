# Configuration Guide

## Environment Variables

Copy `.env.example` to `.env` and fill in:

```
VITE_SUPABASE_URL=https://your-project.supabase.co
VITE_SUPABASE_ANON_KEY=your-anon-key
VITE_SITE_URL=https://your-hackathon.example.com
```

## Content Configuration

### i18n files (`src/i18n/en.ts` and `src/i18n/zh.ts`)

These files contain ALL user-facing text. Search for `[` to find all placeholders that need replacing:

- `[EVENT_NAME]` — Your hackathon name
- `[ORGANIZER]` — Your organization name
- `[EVENT_TAGLINE]` — Your tagline
- `[EVENT_DATES]` — e.g. "June 15-16, 2026"
- `[VENUE]` — Venue name
- `[CITY]` — City name
- `[PARENT_EVENT]` — Parent conference name (if applicable)
- `[DATE]` — Specific dates in schedule

### Countdown Timer

In `src/components/sections/HeroSection.vue`, update the two ISO 8601 timestamps:
```ts
const { days, hours, minutes, seconds, isLive, isOver } = useCountdown(
  '2026-06-15T09:00:00+02:00',  // Event start
  '2026-06-16T20:00:00+02:00'   // Event end
)
```

### Sponsor Logos

1. Place logo files in `public/sponsors/`
2. Update `HeroSection.vue`, `SponsorsSection.vue`, and `TechSection.vue` with `<img>` tags pointing to your logos

### Awards

Edit `PrizesSection.vue` to configure your award structure. Update the corresponding keys in the i18n files.

### Event Photos

Place photos in `public/photos/`:
- `hero-bg.mp4` + `hero-bg-poster.jpg` — Hero background video
- `venue.jpg` — Venue photo
- `event-*.jpg` — Past event photos for the venue section photo wall

### Admin Password

The admin page uses a SHA-256 hash stored in the `admin_config` Supabase table. To set your admin password:

```sql
INSERT INTO admin_config (key, value)
VALUES ('admin_pass_hash', encode(sha256('your-password-here'), 'hex'))
ON CONFLICT (key) DO UPDATE SET value = EXCLUDED.value;
```

### Email Notifications

The Supabase Edge Function `send_team_email` handles email notifications. Configure:
- `SMTP_HOST`, `SMTP_PORT` — Your SMTP server
- `SMTP_USER`, `SMTP_PASS` — SMTP credentials
- `SITE_URL` — Your site URL

Update the email template branding in `supabase/functions/send_team_email/index.ts`.
