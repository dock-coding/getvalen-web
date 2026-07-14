# getvalen-web

Static site for `getvalen.app`. Deployed on Cloudflare Pages. No build step, no framework, no dependencies.

```
index.html      Landing page — keeps the domain root from 404ing
privacy.html    Privacy Policy — served at /privacy
styles.css      Shared stylesheet
```

## Deploy (Cloudflare Pages)

1. Push this to `dock-coding/getvalen-web` on GitHub
2. Cloudflare → **Workers & Pages** → **Create** → **Pages** → **Connect to Git** → pick the repo
3. Build settings: **framework preset: none**, **build command: (blank)**, **output directory: `/`**
4. Deploy. Check the `*.pages.dev` URL works
5. **Custom domains** → add `getvalen.app` and `www.getvalen.app`. DNS is already at Cloudflare, so it wires the records itself
6. Confirm `https://getvalen.app/privacy` loads

Cloudflare Pages serves `privacy.html` at `/privacy` automatically — no config needed.

While you're in the dashboard: **SSL/TLS → Full (strict)**, and **Edge Certificates → Always Use HTTPS: On**.

## ⚠️ Before publishing

The page ships with a **red DRAFT banner** and **yellow-highlighted placeholders**. Both are deliberate — if one escapes to production, you will see it immediately.

**Fill every placeholder:**

| Placeholder | Source |
|---|---|
| `[DATE]` ×2 | Publication date |
| `[COMPANY NAME]` ×3 | Companies House |
| `[COMPANY NUMBER]` | Companies House |
| `[REGISTERED OFFICE ADDRESS]` ×2 | Companies House — **must match the D-U-N-S and Play records** |
| `[ICO NUMBER]` | ICO registration |
| `[TRANSFER MECHANISM — VERIFY]` | Anthropic's DPA |
| `[ANTHROPIC RETENTION PERIOD — VERIFY]` | Anthropic's DPA |
| `[16 / 18 — DECIDE]` | Your call |

**Verify, don't assume:**

1. **Anthropic's transfer mechanism** (UK IDTA vs EU SCCs) and **API retention period**. Both are asserted nowhere in this draft on purpose — a wrong claim in a legal document is worse than an obvious gap.
2. **The no-training claim in §4.3.** It's one of the strongest statements on the page. It must be true.

**Then:**

- [ ] Delete the entire `<div class="draft-banner">` block in `privacy.html`
- [ ] Search the repo for `[` — there should be no `[PLACEHOLDER]` left
- [ ] Search for `class="ph"` — there should be none left
- [ ] Swap the placeholder `<svg>` wordmark for the real faceted **V** mark from the app (two files: `index.html`, `privacy.html`)

## Blocked on

**§5 (health data / explicit consent) describes a consent mechanism the app does not yet have.** Part 39 Pass 1 adds it at the auth gate. **Do not publish this policy until that ships** — a published claim that isn't true is worse than no policy.

## Notes on the design

The palette is semantic, not decorative. **Pine** = data that stays on your device. **Ochre** = data that leaves it. Nothing else on the page is coloured. The "boundary" block in §00 is the only bold moment — everything around it is deliberately quiet, because the strongest thing Valen has to say about privacy is a single sentence, and the design's job is to let it land.

Solid chips are held by you; dashed, outlined chips are held by someone else. The fill carries the meaning, so there is no legend.
