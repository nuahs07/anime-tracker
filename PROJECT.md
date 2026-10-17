# PROJECT.md: Anime & Manga Tracker (MAL-connected)

> Paste this at the start of any AI chat or keep it in the repo root so every tool has the same context.

## Goal
- Web app that tracks anime and manga, synced with my MyAnimeList (MAL) account
- Portfolio project for backend and cloud/DevOps roles, so backend quality and deployment matter as much as the UI

## Features
- MAL login (OAuth2 with PKCE) and list sync
- View and update progress, status, and ratings
- Stats dashboard with charts (genres, scores, episodes watched, etc.)
- Airing schedule filtered to my Watching list
- Recommendations (MAL suggestions and per-anime recommendations)
- AI recommendations: an LLM suggests what to watch or read next based on my list, ratings, and taste (Gemini API free tier)
- Light and dark mode with a toggle (remember my choice, default to system setting)
- New season tracker: if I started an anime and a sequel is announced or airing, notify me automatically
- More features to be added later (etc.): search, filters, responsive and mobile-friendly layout, manga tracking, and anything else that fits

## Stack
- Frontend: Next.js, Tailwind (with dark mode support), Recharts
- Backend: FastAPI (Python)
- Database: PostgreSQL (Neon or Supabase free tier)
- External APIs: MAL API v2 (auth and my list), Jikan (airing schedule and extra data), Gemini API (AI recommendations)
- Hosting: Vercel (frontend), Render (backend)
- DevOps: Docker, GitHub Actions (CI and daily cron), Terraform later

## Architecture
```
Browser (Next.js) -> FastAPI -> PostgreSQL
                        |-> MAL API v2
                        |-> Jikan API
                        |-> Gemini API (AI recommendations)
Daily scheduled job -> check related_anime for sequels -> save notifications
```

## New season tracker logic
1. For each anime in my list (watching or completed), fetch `related_anime`
2. Find entries with relation type "sequel"
3. If the sequel is airing or upcoming and not already in my list or notifications
4. Save a notification

## Build order
1. Repo setup, this file, MAL API client ID
2. MAL OAuth2 login
3. Show my anime list
4. Update progress and ratings
5. Stats dashboard
6. Airing schedule
7. New season tracker and daily job
8. Recommendations (MAL-based, then AI-powered)
9. Light and dark mode polish (can start from step 3)
10. Dockerize, CI, deploy

## Rules for the AI assistant
- Work on ONE step at a time and wait for me before moving on
- Explain what each piece of code does, step by step, in simple terms
- Show complete files or clearly marked changes, not vague snippets
- Never hardcode secrets (client ID, client secret, DB URL); use environment variables and a `.env.example`
- Prefer free-tier services
- Keep the code simple and readable; no over-engineering
- Tell me how to test each step before we continue

## Current status
- [ ] Step 1: repo and MAL app registered
