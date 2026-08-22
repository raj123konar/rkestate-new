[README.md](https://github.com/user-attachments/files/31339026/README.md)
# RK Real Estate Consultant — React (Apollo design system)

Rebuilt as a Vite + React project using the "Apollo" design tokens you provided
(warm cream canvas, espresso-brown structural dark, terracotta accent, thin
serif display type). `MonaSans` and `paradigm-pro` are proprietary fonts, so
this uses the documented substitutes instead: **Inter** for MonaSans and
**Cormorant** (weight 300) for paradigm-pro. Swap the Google Fonts link in
`index.html` for the real font files if you have licenses for them.

## Run it locally

```bash
npm install
npm run dev
```

Opens at `http://localhost:5173`.

## Build for production

```bash
npm run build
```

Outputs static files to `dist/` — this is what you deploy.

## Deploying

This project was **not** tested by running `npm install`/`npm run build` in the
sandbox this was generated in (no internet access there), so please run
`npm install && npm run build` locally first and fix anything that comes up
before deploying.

Recommended: connect this project's folder to a GitHub repo, then import that
repo into Vercel. Every `git push` will then redeploy automatically to your
*same* `rkestate.online` URL — no more drag-and-drop-creates-a-new-project
problem from Vercel Drop.

## Structure

- `index.html` — page shell + all SEO meta tags / JSON-LD
- `public/robots.txt`, `public/sitemap.xml` — served as-is at the site root
- `vercel.json` — SPA rewrite so `/blog/some-post` doesn't 404 on refresh
- `src/main.jsx` — entry point, wraps the app in a router
- `src/App.jsx` — route definitions (`/`, `/blog`, `/blog/:slug`)
- `src/components/` — Nav, Footer, floating WhatsApp/call buttons, per-page SEO helper
- `src/pages/Home.jsx` — the main one-page site (hero → services → process → testimonials → agent → blog preview → contact)
- `src/pages/BlogList.jsx`, `src/pages/BlogPost.jsx` — blog index and individual post pages
- `src/blogPosts.js` — all 12 blog posts as data (title, meta description, date, excerpt, content)

## About the blog

Each post gets its own real URL (`/blog/<slug>`) with its own `<title>` and meta description,
set client-side via `src/components/Seo.jsx`. This is genuinely better for SEO than cramming
everything onto one page, but it is client-side rendering (CSR), not server-side rendering —
Google can index CSR pages, but a framework with real SSR/static generation (like Next.js)
would index faster and more reliably. Worth considering if the blog becomes a bigger priority.

To add a new post, add an entry to the array in `src/blogPosts.js` and it will automatically
appear in the blog list, get its own URL, and show up in `public/sitemap.xml` the next time you
regenerate it.
