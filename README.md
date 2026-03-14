# ChurnLens

> Understand why customers cancel — without paying enterprise prices.

ChurnLens is a lightweight cancellation exit survey tool with AI-powered theme synthesis, built for indie SaaS founders at **$29/mo**.

---

## The problem

Solo SaaS founders have no affordable way to understand *why* customers cancel at a qualitative level:

- **Raaft** — $79/mo (overpriced for sub-$5K MRR products)
- **Churnkey** — $250/mo
- **Baremetrics** add-on — $129/mo

ChurnLens fills the gap: exit interviews + AI theme synthesis at indie-founder pricing.

---

## How it works

1. **Connect Stripe** — paste a restricted API key or use OAuth (60 seconds)
2. **Customer cancels** — ChurnLens intercepts the webhook, sends a 3-question survey email within 5 minutes
3. **You get clarity** — every Monday: top themes, representative quotes, MRR impact in a plain-English digest

---

## Tech stack

| Layer | Tech |
|-------|------|
| Frontend | Next.js 14 (App Router) + Tailwind CSS |
| Backend / API routes | Next.js Route Handlers |
| Database | Supabase (Postgres + RLS + Auth) |
| Email | Resend |
| AI | OpenAI GPT-4o-mini |
| Payments | Stripe Billing |
| Hosting | Vercel (frontend + cron) |

---

## Project structure

```
src/
├── app/
│   ├── page.tsx              # Landing page
│   ├── onboarding/           # Stripe connect flow
│   ├── survey/[token]/       # Exit survey (WCAG AA)
│   ├── dashboard/            # Founder response dashboard
│   └── api/
│       ├── webhooks/stripe/  # Stripe event handler
│       ├── survey/           # Survey form submission
│       ├── themes/           # AI clustering cron (Mon 06:00 UTC)
│       └── digest/           # Weekly email cron (Mon 07:00 UTC)
├── lib/
│   ├── supabase.ts
│   ├── stripe.ts
│   ├── resend.ts
│   └── openai.ts
emails/
└── weekly-digest.tsx         # React Email template
supabase/
└── migrations/001_initial.sql
```

---

## Local development

```bash
# 1. Install dependencies
npm install

# 2. Set environment variables
cp .env.example .env.local
# Fill in: SUPABASE, STRIPE, OPENAI, RESEND keys

# 3. Apply DB schema
npx supabase db push

# 4. Start dev server
npm run dev

# 5. Preview email template
npx email dev
```

### Stripe webhook (local)

```bash
stripe listen --forward-to localhost:3000/api/webhooks/stripe
```

---



## License

MIT
