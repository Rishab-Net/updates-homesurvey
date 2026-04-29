# Deploying updates.homesurvey.ai — Voice Notes + AI Move Summary

**For:** Rishab
**Date:** April 3, 2026
**Site:** updates.homesurvey.ai (new site — not yet live)

---

## What This Deploys

A new Vercel site at `updates.homesurvey.ai` with two published feature articles:

1. **Voice Notes with Auto Exclude** (March 27, 2026)
2. **Interactive AI Move Summary** (April 3, 2026)

A third article (Custom Questionnaire) is present in articles.json with `published: false` and will not appear on the index page.

## Deployment Steps

### 1. Create a new Vercel project

- Create a new project in Vercel under the Helix account
- Connect it to a repo (or deploy as a static site)
- Set the custom domain to `updates.homesurvey.ai`
- No build step needed — this is a static site

### 2. DNS setup

Make sure `updates.homesurvey.ai` has a CNAME record pointing to Vercel (e.g., `cname.vercel-dns.com`), or configure it through Vercel's domain settings.

### 3. Deploy from the `updates_release_2_ai_move_summary` folder

This folder contains everything — both articles, the index page, styles, and all config files. Deploy the **entire folder contents** to the project root.

**Use this folder, NOT `updates_release_1_voice_notes`.** Release 2 is a superset that includes everything from Release 1.

```
updates.homesurvey.ai/
├── index.html                                    ← Updates index page
├── article-styles.css                            ← Shared article styles
├── vercel.json                                   ← Vercel routing config
├── robots.txt                                    ← Search engine directives
├── sitemap.xml                                   ← Both article URLs
├── llms.txt                                      ← LLM summary (2 features)
├── llms-full.txt                                 ← LLM full context (2 features)
├── articles/
│   ├── articles.json                             ← Voice notes + AI summary published
│   ├── voice-notes-auto-exclude.html             ← Voice Notes article
│   └── interactive-ai-move-summary.html          ← AI Move Summary article
└── images/                                       ← NOT NEEDED (see note below)
```

### 4. Do NOT deploy the `images/` folder

The article HTML references Mailchimp CDN URLs for all images — they are already live. The `images/` folder is a local backup only.

### 5. Commit and push

```bash
git add index.html article-styles.css vercel.json robots.txt sitemap.xml llms.txt llms-full.txt articles/
git commit -m "Launch updates.homesurvey.ai with Voice Notes and AI Move Summary articles"
git push
```

### 6. Verify after deploy

| URL | Expected |
|-----|----------|
| `https://updates.homesurvey.ai/` | Index page showing 2 articles (Voice Notes + AI Move Summary) |
| `https://updates.homesurvey.ai/articles/voice-notes-auto-exclude/` | Voice Notes article with March 27, 2026 date |
| `https://updates.homesurvey.ai/articles/interactive-ai-move-summary/` | AI Move Summary article with April 3, 2026 date |
| `https://updates.homesurvey.ai/llms.txt` | LLM summary with both features |
| `https://updates.homesurvey.ai/llms-full.txt` | LLM detailed reference with both features |
| `https://updates.homesurvey.ai/sitemap.xml` | Three URLs (index + both articles) |

## Cross-Link Note

Both articles contain inline links to `../custom-questionnaire/`. This will 404 until the Custom Questionnaire article is published in a future release. This is acceptable — they are inline text links, not prominent buttons. Alternatively, temporarily remove those links and restore them later.
