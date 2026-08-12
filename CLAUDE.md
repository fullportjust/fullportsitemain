# Full Port University — Marketing Site

Context for Claude Code. Read this before making changes.

## The point of this project

Full Port University (FPU) is a beginner-friendly options and stock trading education + signals community on Discord, run by Justin Kim and monetized through Whop (a 14-day free trial that converts to paid membership). The core offer is live `[BUY]` → `[TRIM]` → `[SELL]` trade signals from a multi-analyst desk, a free beginner course, and weekly live teaching.

This repo is a high-converting marketing website whose job is to take a cold beginner — someone who has never traded options — and move them into the free Whop trial. Everything on the site serves that funnel. The positioning that makes FPU different from competitors (e.g. Capital Club, a solo-founder swing-trading Discord) is **beginner-first teaching + a multi-analyst desk + options/DTE specialization**. Lead with "you can learn this from zero," use signals and member results as proof, push the free trial hard.

This is a separate, from-scratch site — **not** the legacy WordPress site at fullportuniversity.com, and **not** the other FPU properties (the Framer funnel, the mentorship page, the onboarding app). It is intended to eventually become fullportuniversity.com, but currently deploys to a Vercel staging URL.

## Tech stack & structure

- Plain static HTML/CSS/JS. No framework, no build step. Each page is a self-contained `.html` file with inline `<style>` and a small inline `<script>`.
- `vercel.json` provides `cleanUrls` (so `/how-it-works` serves `how-it-works.html`) and security headers.
- Pages: `index.html` (home), `how-it-works.html`, `education.html`, `how-to-read-a-trade-signal.html` (a guide/blog article), `404.html`.
- No pricing page — it was intentionally dropped; every trial CTA links straight to `https://whop.com/fullportuniversity/`.
- Shared shell (nav, footer, `<head>` CSS, risk strip, JSON-LD) is duplicated across every page because there's no templating. **When you change the nav/footer/CSS, change it in all pages consistently.**

## Design system

- **Aesthetic:** dark trading-terminal.
- CSS tokens live in `:root`. Key colors: `--green:#12E27C` (primary/buy), `--gold:#F5C451` (VIP/trial accent), dark navy surfaces, muted grays for text.
- **Fonts:** Space Grotesk (headlines), Inter (body), JetBrains Mono (data/tags/signals).
- **Signal tag colors:** BUY = green, TRIM = cyan (`#7FE0FF`), SELL = purple (`#C9A6FF`).
- **Reusable classes:** `.wrap` (max-width container), `.section`, `.btn` / `.btn--primary` / `.btn--lg` / `.btn--ghost`, `.eyebrow`, `.hl` (highlight), `.faq` / `details`, `.chip`, `.wins-wall` (masonry), `.riskstrip`, `.trial-band`.

## Hard rules (do not violate)

- **Compliance** (this is YMYL / financial content). Every page must keep the header risk strip and the footer risk disclosure. Language stays: "educational only," "not financial advice," "not a registered investment advisor," "results not typical." Never add "no credit card required" (Whop captures payment; it would be false). Never frame the trial as a profit guarantee — the approved framing is "14 days free, cancel anytime before day 14, never charged."
- **Authenticity is non-negotiable.** Profit/results imagery must be real screenshots from the Discord `#post-profits` channel with accurate figures — never fabricated composites, never inflated numbers, never duplicated trades presented as different ones.
- **Signal system on this site is three steps:** `[BUY]` → `[TRIM]` → `[SELL]`. (Older FPU properties reference a `[LOAD]` step — this site does not use it.) Position sizing tiers: FULL / SMALL / LOTTO. Risk framed around DTE (days to expiration).
- **Member count:** use "10,000+." Other FPU properties show inconsistent figures (4,500 / 7,000) — flag, don't copy.
- **Images:** content images (profit screenshots, etc.) are external, optimized, lazy-loaded files — not base64. The logo is a single external `logo.png` (cached across pages). Keep pages light; don't re-embed large base64.

## SEO / AEO (already implemented — maintain it)

- JSON-LD on every page: `Organization` (with `sameAs`), plus `WebSite` + `FAQPage` on home, `Course` on education, and `Article` + `FAQPage` + `BreadcrumbList` on the guide. Keep it valid JSON and keep FAQ schema mirroring the visible FAQ text.
- `sitemap.xml`, `robots.txt` (explicitly welcomes AI crawlers: GPTBot, ClaudeBot, PerplexityBot, etc.), and `llms.txt` exist at root.
- Canonical / OG / sitemap URLs all use `https://fullportuniversity.com/` — correct only once this site IS that domain. **On the staging Vercel URL, do not submit the sitemap to Search Console.**
- **Strategy:** don't chase head terms ("options trading"); win long-tail + Discord + brand/comparison terms via content. Keyword/content plan lives in `FPU-seo-aeo-plan.md` (kept outside the repo). The first article (`how-to-read-a-trade-signal.html`) is done.

## Key facts

- CTAs → `https://whop.com/fullportuniversity/`
- Support email: `growth@fullportuniversity.com`
- Socials in schema + footer: Instagram `@fullportuniversity.just`, TikTok `@fullport.just`. (No public X / YouTube / Discord-invite URL on record yet.)
- Mentorship program link: `https://fpumentorship.vercel.app/`

## ⚠️ Open items / roadmap

1. ~~**UNRESOLVED: pricing.**~~ **RESOLVED 2026-08-12:** Justin confirmed the price is **$99/month**. The "$99/year" figure on record elsewhere is wrong — do not "correct" the site to it. Current copy in `index.html` (hero micro-line and trial band) already says `$99/month` and is correct.
2. VSL embed is a placeholder (`#vsl` block) — needs a real video URL or removal.
3. Add internal links to `how-to-read-a-trade-signal.html` from How It Works and Education (helps it rank).
4. Build the remaining long-tail articles from the content plan (clusters: Discord options trading, Discord/trading signals, stock trading, beginner options, brand/comparison).
5. Build a Results/Reviews page (identified gap — would own the brand SERP).
6. Add X / YouTube / Discord-invite URLs to the Organization `sameAs` once available.
7. Minor: `og-image.png` renders star glyphs as tofu boxes; logo wordmark uses a placeholder typeface.

## Workflow

Static site → GitHub repo → Vercel git integration → auto-deploy on push. Claude Code handles the codebase (edits, new pages, commits, deploys). Claude chat handles strategy, copywriting, the keyword/content plan, and generating image assets, then hands finished content here to be wired in.

## How Justin communicates

Justin often writes via voice transcription, so expect phonetic approximations of technical terms: "Verso"/"Versal" = Vercel, "WAP"/"swap" = Whop, "weball" = Webull, "fan bases" = Fanbasis, "magistrate" = mentorship. Interpret by context.
