# AGENTS.md

## Purpose

This repository publishes Leo Bergmann's public author website and a Pinterest-compatible RSS feed. Its job is to turn approved book material into useful reader-facing teasers that lead to the corresponding Amazon book page. The current campaign focuses on the Airfryer cookbook, but the structure may be extended to other books and social channels.

These instructions apply to the entire repository.

## Sources of truth

Book production sources are outside this public repository:

- Book library: `C:\Daten\src\python\BookGenPy\library`
- KDP product projects: `C:\Daten\src\python\BookGenPy\products\kdp`
- Local marketing control project and dashboard: `C:\Daten\src\python\marketing_codex` and `http://127.0.0.1:8765/`

Read those sources when a task requires accurate book metadata or content. Do not edit book production files unless the task explicitly includes that work. Copy only material that is suitable and licensed for public use.

## Repository map

- `site_config.json`: public site metadata, Amazon destination, RSS metadata, and Pinterest verification.
- `content/recipes.json`: scheduled public items and their metadata.
- `assets/`: publishable cover and social images.
- `build.py`: deterministic static-site and RSS generator.
- `styles.css`: source stylesheet.
- `docs/`: generated GitHub Pages output; never edit it by hand.
- `tests/`: public-output, RSS, link, and Pinterest verification checks.
- `.github/workflows/publish.yml`: scheduled build and publication workflow.

## Public-content boundaries

- Write for readers. Never expose budgets, campaign notes, scheduler state, account setup details, credentials, private email addresses, tokens, browser data, customer data, or internal file inventories.
- Never commit `credentials.vault.json`, `.env`, cookies, browser profiles, exported credentials, or secrets.
- Keep credentials and account recovery data outside this public repository. GitHub Actions secrets are appropriate only when an integration genuinely needs them.
- Do not invent testimonials, ratings, health claims, book contents, discounts, availability, or performance results.
- Avoid spam, repetitive near-duplicates, unsolicited messages, and engagement manipulation.
- Paid actions require explicit current authorization. A public page must never describe internal spending limits.
- Preserve the Pinterest verification meta tag unless ownership intentionally changes.
- Keep Amazon links sponsored/nofollow in rendered HTML. Update the destination centrally in `site_config.json`, not in generated pages.
- Each RSS item must use a canonical URL on the claimed website and an absolute public image URL.

## Creating a recipe item and Pinterest Pin

Pinterest imports the RSS title, description, destination page, and `media:content` image. To add an item:

1. Inspect the relevant book source and choose a truthful teaser. Do not publish a full paid recipe or substantial book excerpt without explicit approval.
2. Create or select a publishable, rights-cleared image. Prefer a square high-quality JPEG around 1000 x 1000 pixels for this feed and place it under `assets/recipes/`.
3. Append an object to `content/recipes.json` with a unique, stable `id`, reader-facing `title` and `description`, optional `prep`, `cook`, `servings`, and `difficulty`, a repository-relative `image`, and an ISO-8601 UTC `publish_at`.
4. Use natural German, useful search terms, and genuinely distinct copy. The description must make sense on both the page and Pinterest.
5. Schedule only within the requested campaign window. Confirm UTC conversion when the requested time is local Europe/Berlin time.
6. Build and test. Confirm that the generated page, image, canonical URL, feed entry, and Amazon destination all work.

For a native Pin or another social network, use the generated public page as the destination, adapt the image dimensions and copy to that platform, and keep account operations outside this repository. Prefer official APIs or platform-supported schedulers. Do not automate CAPTCHA, phone, email, or identity verification.

## Build and verification

Run from the repository root:

```powershell
python build.py
python -m unittest discover -s tests -v
python -m http.server 8080 --directory docs
```

For a reproducible preview, use `python build.py --now 2026-07-21T18:00:00Z`. Before publishing:

- inspect `git status` and the complete diff;
- run the full test suite;
- visually inspect the home page, privacy page, one item page, and a narrow viewport;
- confirm public HTML and RSS contain no operational or secret markers;
- verify RSS XML, target pages, images, canonical links, Pinterest verification, and the Amazon URL;
- keep generated `docs/` in sync with its sources.

## Deployment

GitHub Pages serves `docs/` from `main`. The workflow checks due content at 03:15 and 14:15 UTC, rebuilds the site, runs tests, and commits only changed generated output. RSS build dates are deterministic, so the feed remains unchanged after the last scheduled item.

Because the workflow can commit to `main`, run `git pull --ff-only` before new publication work and again if a push is rejected. After pushing, verify both the workflow and the public URLs:

- Website: https://leanovich.github.io/leo-bergmann-books/
- RSS: https://leanovich.github.io/leo-bergmann-books/feed.xml
- Repository: https://github.com/leanovich/leo-bergmann-books

## Current campaign context

The existing Airfryer vacation campaign schedules two RSS items per day from 22 through 29 July 2026. Treat these dates as campaign-specific historical configuration, not a permanent rule. Extend or replace them only when the requested campaign scope changes.
