# Personal Site — Project Specification

## Overview

A warm, personal website that serves as a multi-discipline freelance showcase. The site establishes credibility and attracts client leads by combining a portfolio of work, a blog, a resume/CV, and an about page — all presented with a human, approachable aesthetic.

**Primary goal:** Convert visitors into freelance inquiries.  
**Audience:** Potential clients evaluating you for a project.

---

## Pages & Information Architecture

### Launch scope (MVP)

| Page | Route | Purpose |
|------|-------|---------|
| Home | `/` | Hero intro, value proposition, selected work, call-to-action |
| About | `/about` | Story, background, skills, what you offer, photo |

### Post-launch (Phase 2)

| Page | Route | Purpose |
|------|-------|---------|
| Portfolio | `/work` | Grid of projects |
| Project detail | `/work/[slug]` | Case study: problem, process, outcome |
| Blog | `/blog` | Article index with tags or categories |
| Post detail | `/blog/[slug]` | Full article with reading time, metadata |
| CV / Resume | `/cv` | Printable-friendly credentials page |

---

## Design Direction

**Aesthetic:** Warm and personal — approachable, human, with distinct personality. Not corporate, not purely minimal.

**Principles:**
- Typography-forward: expressive headings, comfortable reading measure
- Accent color carries personality; backgrounds stay neutral/warm
- Generous whitespace — never cluttered
- Content loads instantly; no skeletons or layout shifts

**References to gather before implementation:**
- Select 2–3 personal sites you admire and note what works
- Define: primary font (serif or humanist sans), accent color, neutral palette

---

## Tech Stack

| Layer | Choice | Rationale |
|-------|--------|-----------|
| Framework | SvelteKit 2 + Svelte 5 | Already scaffolded; reactive, fast, excellent DX |
| Language | JavaScript (jsconfig) | Existing project uses JS, not TS — keep consistent |
| Styling | TailwindCSS v4 | Utility-first, pairs well with Svelte; fast iteration |
| CMS | **Sanity** | Generous free tier, real-time, excellent SvelteKit integration, GROQ is powerful |
| Hosting | Vercel | Zero-config SvelteKit deploys via `@sveltejs/adapter-vercel` |
| Images | Sanity CDN + `@sanity/image-url` | Automatic transforms, responsive images |
| Local dev | Docker + Docker Compose | Isolated dev environment; no host machine side-effects |

---

## Content Model (Sanity)

### `project` document
```
title        string
slug         slug
summary      text (short)
coverImage   image
tags         array<string>
disciplines  array<string>   // e.g. "Design", "Development"
publishedAt  date
body         portableText
featured     boolean         // surfaces on home page
```

### `post` document
```
title        string
slug         slug
excerpt      text (short)
coverImage   image
tags         array<string>
publishedAt  date
body         portableText
```

### `page` document (About, CV)
```
title        string
slug         slug
body         portableText
```

### `siteSettings` singleton
```
name         string
tagline      string
bio          text
avatar       image
socialLinks  array<{platform, url}>
```

---

## Key Components

| Component | Notes |
|-----------|-------|
| `Header` | Logo/name + nav links; sticky or scroll-away |
| `Footer` | Minimal: name, social links, year |
| `ProjectCard` | Cover image, title, discipline tags, brief summary |
| `PostCard` | Title, date, excerpt, read time |
| `PortableText` | Sanity block content renderer |
| `SEO` | `<svelte:head>` wrapper for title, description, OG tags |

---

## SEO

**Scope:** Moderate — correct fundamentals, no advanced structured data at launch.

- Unique `<title>` and `<meta name="description">` on every page
- Open Graph tags (`og:title`, `og:description`, `og:image`) for social sharing
- Canonical URLs
- Readable URL slugs (all driven by Sanity slug fields)
- `robots.txt` and basic `sitemap.xml` (static or generated at build)
- No JSON-LD at launch

---

## Performance

- `@sveltejs/adapter-vercel` with prerendering for static pages (home, about, CV)
- Blog and portfolio pages: ISR (incremental static regeneration) or SSR with Vercel edge caching
- Images served via Sanity CDN with `?w=` and `?fm=webp` transforms
- No client-side JS hydration for purely content pages where possible

---

## Local Development (Docker)

The dev environment runs entirely inside a container so nothing — Node, npm cache, `node_modules` — pollutes the host machine.

### Design constraints
- The container runs only for **local development**; Vercel builds and runs production natively (no container involved).
- `node_modules` lives inside the container volume, not bind-mounted from the host, so host and container Node versions never conflict.
- Source files (`src/`, `static/`, config files) are bind-mounted so edits on the host are reflected instantly via Vite HMR.
- Port `5173` (Vite dev server) is forwarded to the host.

### File structure
```
docker-compose.yml       # orchestrates the dev service
Dockerfile.dev           # Node image + installs deps on first run
.env                     # local secrets (gitignored)
.env.example             # committed template with all required keys
```

### `Dockerfile.dev`
```dockerfile
FROM node:22-alpine
WORKDIR /app
# deps installed at container start via entrypoint, not image build,
# so package.json changes don't require a full image rebuild
COPY package*.json ./
RUN npm ci
```

### `docker-compose.yml`
```yaml
services:
  app:
    build:
      context: .
      dockerfile: Dockerfile.dev
    ports:
      - "5173:5173"
    volumes:
      - .:/app                        # bind-mount source
      - /app/node_modules             # anonymous volume shadows host node_modules
    environment:
      - NODE_ENV=development
    env_file:
      - .env
    command: npm run dev -- --host 0.0.0.0
```

The `--host 0.0.0.0` flag is required so Vite listens on all interfaces inside the container, not just localhost.

### Vercel compatibility
`adapter-auto` (or `adapter-vercel` once switched) is only invoked at **build time**, not during `npm run dev`. The dev container never runs the adapter, so there is no conflict. Vercel's build pipeline ignores Docker entirely — it clones the repo, runs `npm ci` + `npm run build` in its own environment, and deploys the output.

### Environment variables
| Variable | Local | Vercel |
|----------|-------|--------|
| `SANITY_PROJECT_ID` | `.env` (gitignored) | Vercel dashboard |
| `SANITY_DATASET` | `.env` | Vercel dashboard |
| `SANITY_API_VERSION` | `.env` | Vercel dashboard |
| `PUBLIC_BASE_URL` | `.env` | Vercel dashboard (auto-set via `VERCEL_URL`) |

Commit `.env.example` with placeholder values; never commit `.env`.

---

## Deployment

1. Connect GitHub repo to Vercel project
2. Add environment variables: `SANITY_PROJECT_ID`, `SANITY_DATASET`, `SANITY_API_VERSION`
3. Use `@sveltejs/adapter-vercel` (replace `adapter-auto`)
4. Preview deploys on every PR; production on `main`

---

## Development Phases

### Phase 1 — Foundation (now)
- [ ] Add `Dockerfile.dev`, `docker-compose.yml`, `.env.example`, and `.dockerignore`
- [ ] Add `node_modules/` and `.env` to `.gitignore`
- [ ] Verify `npm run dev -- --host 0.0.0.0` works inside container with HMR
- [ ] Install and configure TailwindCSS v4
- [ ] Define design tokens (colors, fonts, spacing)
- [ ] Implement `Header` and `Footer`
- [ ] Build `/` (Home) with static content
- [ ] Build `/about` with static content
- [ ] Add `SEO` component
- [ ] Configure Vercel deploy + custom domain

### Phase 2 — CMS integration
- [ ] Create Sanity project + studio
- [ ] Define content schemas (project, post, siteSettings)
- [ ] Wire Sanity client into SvelteKit load functions
- [ ] Build `/work` + `/work/[slug]`
- [ ] Build `/blog` + `/blog/[slug]`
- [ ] Build `/cv`
- [ ] Migrate static home/about content into Sanity

### Phase 3 — Polish
- [ ] Responsive testing across breakpoints
- [ ] Sitemap + robots.txt
- [ ] OG image generation (optional: `@vercel/og` or static)
- [ ] Accessibility audit (keyboard nav, color contrast)
- [ ] Analytics (Fathom or Plausible — privacy-friendly)

---

## Open Questions

1. **Your name / domain** — What will the site be called? This affects `siteSettings` defaults and Vercel domain config.
2. **Disciplines** — What are the 2–4 services you offer freelance? (e.g. "Product Design", "Frontend Development", "Brand Strategy") — these become portfolio filter tags and homepage messaging.
3. **Font selection** — Any typeface preferences, or should a warm humanist pair be proposed?
4. **Contact method** — No form at launch, but how should clients reach you? Email link? LinkedIn? Calendly?
5. **Analytics** — Do you want any traffic tracking at launch?
