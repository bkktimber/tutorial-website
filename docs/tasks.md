# Phase 1 — Foundation Tasks

## 1. Docker Dev Environment
- [x] Remove `.devcontainer/`
- [x] Create `Dockerfile.dev`
- [x] Create `docker-compose.yml`
- [x] Create `.env.example`
- [x] Create `.dockerignore`
- [x] Verify `.gitignore` has `node_modules/` and `.env`

## 2. TailwindCSS v4 + Design Tokens
- [x] Install `tailwindcss` and `@tailwindcss/vite` (inside container)
- [x] Update `vite.config.js` with Tailwind plugin
- [x] Rewrite `app.css` with `@import "tailwindcss"`, `@theme` tokens, base styles

## 3. Vercel Adapter
- [x] Install `@sveltejs/adapter-vercel`, remove `adapter-auto`
- [x] Update `svelte.config.js`

## 4. Components
- [x] Rewrite `Header.svelte` (Svelte 5, Tailwind, active link)
- [x] Rewrite `Footer.svelte` (Svelte 5, Tailwind)
- [x] Create `SEO.svelte`

## 5. Layout
- [x] Update `+layout.svelte` to Svelte 5 runes

## 6. Pages
- [x] Build Home page (`/`) with hero, selected work, CTA
- [x] Build About page (`/about`) with story, skills, photo

## 7. Verification
- [x] `docker compose up --build` — container starts
- [x] Both pages render correctly in browser
- [x] SEO meta tags present in `<head>` (via SEO component)
- [x] `npm run build` succeeds inside container (adapter-vercel ✔)
- [x] HMR works (confirmed via Vite logs)
