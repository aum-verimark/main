# Coming-soon page

Static site. No build step, no framework, no database, no third-party requests (fonts are self-hosted).

```
index.html     the page (styles and script inline)
favicon.svg    tab icon
og.png         image shown when the link is shared (WhatsApp, LinkedIn, X)
fonts/         Instrument Serif, Schibsted Grotesk, IBM Plex Mono (OFL licensed)
vercel.json    caching + basic security headers
```

## Deploy (GitHub → Vercel)

1. Create a new GitHub repo and push these files to the root.
2. In Vercel: **Add New → Project → Import** the repo.
   Framework preset: **Other**. Build command: none. Output directory: leave blank (root).
3. Deploy. Add your domain under **Settings → Domains**.

Every push to `main` redeploys automatically.

## How the "come back" mechanic works

- Each visitor's browser remembers which **days** they visited (localStorage, nothing sent anywhere).
- One of the four words (Connect / Verify / Engage / Grow) unlocks per distinct day visited.
- The countdown runs to the visitor's local midnight, which is when the next word becomes available.
- Clearing browser data or switching devices starts the visitor over at day 1.

To test: open DevTools → Console → `localStorage.removeItem('pv-record-v1')` to reset, or
`localStorage.setItem('pv-record-v1', JSON.stringify({visits:3,days:['2026-01-01','2026-01-02'],seen:2}))` then reload to see day 3.

## Common edits

- **Headline:** search `Reach is everywhere` in `index.html`.
- **Add the brand name:** put it next to the logo mark in `<header class="bar">`, and in `<title>`.
- **Turn off the daily unlock (show everything):** in the script, change `Math.min(4, rec.days.length)` to `4`.
- **Colours:** the `:root` variables at the top of the `<style>` block.

## Later: email capture with Supabase

There is deliberately no form yet. When you want one, add a `waitlist` table in Supabase with RLS allowing
anonymous `insert` only, and post to it from a small form above the countdown.
