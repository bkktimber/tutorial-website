# Phase 1 — Foundation Implementation

Implement all Phase 1 items from `SPEC.md`: Docker dev environment, TailwindCSS v4, design tokens, Header/Footer, Home page, About page, SEO component, and Vercel adapter.

## User Review Required

> [!IMPORTANT]
> The spec's **Open Questions** (lines 247–254) affect placeholder content I'll use throughout Phase 1. I'll proceed with sensible defaults below — please flag anything that's wrong.

| Question | Default I'll use |
|----------|-----------------|
| **Site name** | "Mai" (from your macOS username) |
| **Disciplines** | "Design" and "Development" |
| **Font** | **Instrument Serif** for headings (warm, editorial) + **Inter** for body (clean, readable) |
| **Contact method** | Email link (`mailto:hello@example.com`) |
| **Nav links (MVP)** | Home, About (matching spec — no `/work`, `/blog`, `/contact` until Phase 2+) |

> [!WARNING]
> I will **remove the existing `.devcontainer/` directory** since the spec replaces it with a `Dockerfile.dev` + `docker-compose.yml` approach. Let me know if you want to keep it alongside.

## Open Questions

1. **Accent color** — The existing `app.css` uses a blue-indigo (`#646cff`). The spec says *"warm and personal"*. I'll switch to a warm terracotta/amber accent (e.g. `#c2703e`). OK?
2. **About page photo** — Should I generate a placeholder avatar image, or leave it as a text-only placeholder?
3. **Vercel deploy** — Do you want me to actually run `vercel` CLI setup, or just swap the adapter and leave you to connect the repo manually on vercel.com?

---

## Proposed Changes

### 1. Docker Dev Environment

Remove `.devcontainer/` and add the spec's Docker setup.

#### [DELETE] [devcontainer.json](.devcontainer/devcontainer.json)

#### [NEW] [Dockerfile.dev](Dockerfile.dev)
Minimal `node:22-alpine` image. Copies `package*.json` and runs `npm ci`.

#### [NEW] [docker-compose.yml](docker-compose.yml)
Single `app` service matching the spec exactly (bind-mount source, anonymous volume for `node_modules`, port 5173, `--host 0.0.0.0`).

#### [NEW] [.env.example](.env.example)
Template with all Sanity env vars as placeholders.

#### [NEW] [.dockerignore](.dockerignore)
Exclude `node_modules`, `.svelte-kit`, `.git`, etc.

#### [MODIFY] [.gitignore](.gitignore)
- Verify `node_modules/` and `.env` are already present ✅ (they are)
- No changes needed.

---

### 2. TailwindCSS v4 + Design Tokens

#### Install dependencies (inside container)
```bash
npm install tailwindcss @tailwindcss/vite
```

#### [MODIFY] [vite.config.js](vite.config.js)
Add `@tailwindcss/vite` plugin **before** `sveltekit()`.

#### [MODIFY] [app.css](src/app.css)
Full rewrite:
- `@import "tailwindcss";` at the top
- `@theme` block with design tokens from the spec:
  - **Colors**: warm neutral palette (cream/off-white bg, charcoal text, terracotta accent)
  - **Fonts**: Instrument Serif (headings), Inter (body)
  - **Spacing**: keep existing scale
  - **Radius, transitions**: preserve existing values
- Base layer overrides for `body`, headings, links
- Google Fonts `@import` for Instrument Serif + Inter

---

### 3. Header & Footer

#### [MODIFY] [Header.svelte](src/lib/components/Header.svelte)
- Convert from Svelte 4 (`export let`) to **Svelte 5 runes** (`$props()`)
- Sticky navigation bar with site name + nav links (Home, About)
- Tailwind utility classes for layout
- Mobile hamburger menu (CSS-only toggle or minimal JS)
- Active link indicator using SvelteKit's `$page.url.pathname`

#### [MODIFY] [Footer.svelte](src/lib/components/Footer.svelte)
- Minimal: name, social links (GitHub, LinkedIn), © year
- Tailwind utilities
- Svelte 5 runes

---

### 4. SEO Component

#### [NEW] [SEO.svelte](src/lib/components/SEO.svelte)
- Accepts `title`, `description`, `ogImage`, `canonicalUrl` as props
- Renders `<svelte:head>` with:
  - `<title>`, `<meta name="description">`
  - Open Graph: `og:title`, `og:description`, `og:image`, `og:url`
  - Twitter card meta tags
  - Canonical `<link>`

---

### 5. Layout Update

#### [MODIFY] [+layout.svelte](src/routes/+layout.svelte)
- Update to Svelte 5 `{@render children()}` pattern
- Import `app.css` (already done)
- Wrap content with Header/Footer
- Use Tailwind for page container

---

### 6. Home Page (`/`)

#### [MODIFY] [+page.svelte](src/routes/+page.svelte)
Static content matching the spec:
- **Hero section**: Name, tagline, brief value proposition
- **Selected work**: 2–3 placeholder project cards (static, no CMS yet)
- **Call-to-action**: "Let's work together" with email link
- SEO component with homepage metadata

---

### 7. About Page (`/about`)

#### [NEW] [+page.svelte](src/routes/about/+page.svelte)
Static content:
- Story / background section
- Skills & what you offer (using the disciplines)
- Photo placeholder or generated image
- SEO component with about-page metadata

---

### 8. Vercel Adapter

> [!NOTE]
> **Container compatibility:** `adapter-vercel` is only invoked during `npm run build`, never during `npm run dev`. The dev container runs Vite's dev server directly, so there is zero conflict. Vercel's own production build pipeline ignores Docker entirely — it clones the repo and runs `npm ci` + `npm run build` in its own environment. We will verify that `npm run build` succeeds inside the container as well for local build testing.

#### Install (inside container)
```bash
npm install -D @sveltejs/adapter-vercel
npm uninstall @sveltejs/adapter-auto
```

#### [MODIFY] [svelte.config.js](svelte.config.js)
Switch import from `adapter-auto` to `adapter-vercel`.

---

## Verification Plan

### Automated Tests
1. `docker compose up --build` — container starts, `npm run dev -- --host 0.0.0.0` runs without error
2. Open `http://localhost:5173` in the browser — site loads with new design
3. Navigate `/` and `/about` — both render with correct content and SEO meta tags
4. Verify HMR by editing a file and confirming hot reload
5. `npm run build` inside container — confirms Vercel adapter produces output without errors

### Manual Verification
- Visual inspection of both pages at desktop and mobile widths
- Check `<head>` for correct SEO meta tags via browser DevTools
