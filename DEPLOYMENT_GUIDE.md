# HealthMatch Sage Deployment Guide

## 1. Prerequisites
- Node.js 18+
- npm
- Supabase project configured
- Vercel project (or equivalent static host)

## 2. Local Setup
```bash
npm i
npm run dev
```

## 3. Build Validation
```bash
npm run lint
npm run build
```

## 4. Required Environment Variables

### Frontend/Supabase
- `VITE_SUPABASE_URL`
- `VITE_SUPABASE_ANON_KEY`

### Edge Function Integrations
- `GEMINI_API_KEY`
- `TWILIO_ACCOUNT_SID`
- `TWILIO_AUTH_TOKEN`
- `TWILIO_PHONE_NUMBER`
- `SUPABASE_SERVICE_ROLE_KEY`
- `SUPABASE_URL`
- `BASE_URL`

## 5. Deployment Architecture
- Vercel serves SPA (`vercel.json` rewrite to `/index.html`).
- Supabase hosts DB, Auth, and edge functions.
- External services: Gemini (AI), Twilio (voice workflows).

## 6. Post-Deployment Checklist
- Validate login/signup + protected routes.
- Validate health check and appointment booking flows.
- Validate emergency-call function and webhook updates.
- Validate RLS by testing patient vs doctor data access.
- Monitor edge function logs and error rates.

## 7. Troubleshooting
- **Auth redirect loops:** verify `redirectTo` and allowed domains.
- **Twilio call failures:** verify SID/token/phone env vars.
- **AI function errors:** validate Gemini key + payload shape.
- **Permission denied on DB reads/writes:** review relevant RLS policy.
