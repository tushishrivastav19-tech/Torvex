# TORVEX — Prepare. Progress. Prevail.

TORVEX is an academic-planning and racing-progression PWA foundation. It is designed to be extracted and uploaded into the existing `tushishrivastav19-tech/Torvex` repository.

## Important implementation status

This archive is a runnable, extensible project foundation, **not a claim that every item in the extensive product specification is production-complete**. The current build includes a responsive multi-page React app, local IndexedDB task storage, procedural Three.js vehicle previews, a 30-entry distinct vehicle catalogue, PWA shell caching, Supabase SQL foundations, and authenticated server-side AI Edge Function examples.

The car preview uses procedural shared geometry with per-entry paint and identity metadata. It is not 30 individually sculpted, production-grade vehicle models. The initial academic pages do not yet implement the complete exam syllabus, mock-test authoring, advanced reporting, full plan approval workflow, mission economy, native voice service, full notification scheduler, or complete sync conflict resolution. Those must be implemented and tested before describing the product as fully accepted.

## Requirements

- Node.js 20+
- npm
- Supabase project for authentication, database and Edge Functions (optional for local preview)
- OpenAI API key configured only as a Supabase Edge Function secret for live AI
- Spotify Developer app for Spotify OAuth integration (not wired in this foundation)

## Run locally

```bash
npm install
cp .env.example .env
npm run dev
```

Open the local URL printed by Vite.

Build:

```bash
npm run build
```

## Supabase setup

1. Create a Supabase project.
2. Apply `supabase/migrations/0001_initial.sql` using the Supabase SQL editor or CLI.
3. Add `OPENAI_API_KEY` and optionally `OPENAI_MODEL` as Supabase Edge Function secrets.
4. Deploy functions:

```bash
supabase functions deploy ai-assistant
supabase functions deploy ai-plan
```

5. Add `VITE_SUPABASE_URL` and `VITE_SUPABASE_ANON_KEY` to `.env` for local development and your hosting provider's environment configuration.
6. Never expose service-role keys or AI provider keys in browser variables.

The migration includes user-scoped RLS for personal records. Review and test policies before production deployment.

## AI endpoints

- `ai-assistant`: authenticated assistant conversation; validates message length and calls OpenAI server-side.
- `ai-plan`: authenticated draft plan generation. It returns a draft and explicitly requires user approval before persistence.

These functions require network access, a configured Supabase project and provider credentials. They are not available offline.

## Local-first and PWA

Study tasks are stored in IndexedDB via Dexie. The service worker caches the application shell and same-origin GET requests and handles incoming push events. Browser push delivery while the app is closed requires a push server, VAPID configuration, subscriptions and deployment-specific setup. PWA installability depends on HTTPS (or localhost) and browser support.

## 3D vehicle collection

`src/data/vehicles.ts` contains 30 individually named vehicle collection entries with category, style, paint and level metadata. `src/components/CarScene.tsx` renders an interactive Three.js procedural car preview. Replace the procedural model with individually authored GLB assets to meet a production vehicle-art requirement. The current customization preview supports vehicle paint selection; full body-kit/wheel/accessory persistence is not yet implemented.

## Spotify and voice

The Music Room currently supports saving and opening playlist URLs. Spotify account linking and embedded playback require a Spotify OAuth implementation, app registration and policy-compliant scopes. Voice push-to-talk and speech output are not implemented in this foundation; browser Web Speech API support varies by browser and operating system.

## Deploy

Build with `npm run build`, then deploy `dist/` to a static host supporting SPA fallback. Configure Supabase separately. Serve over HTTPS for PWA install and push support.

## Security and data

- `.env` is intentionally not included.
- `.env.example` contains placeholders only.
- AI secrets belong in Supabase Edge Function secrets.
- IndexedDB data is local to the browser profile and can be lost if site data is cleared.
- Cloud migration and robust offline conflict resolution require additional implementation.

## Existing repository upload

Extract the contents of this archive into the root of the existing `Torvex` repository. Review any repository files before replacing them. Commit and push using the repository owner's normal Git workflow.
