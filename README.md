# Leo Bergmann Books

Public static author site with a Pinterest-compatible RSS feed. The repository contains only publishable marketing content and no credentials.

## Local verification

1. Run `python build.py`.
2. Run `python -m unittest discover -s tests -v`.
3. Serve `docs` with `python -m http.server 8080 --directory docs`.
4. Open `http://127.0.0.1:8080/`.

## GitHub Pages

The intended repository is `leanovich/leo-bergmann-books`. Configure GitHub Pages to publish from the `docs` directory on the `main` branch.

The workflow checks newly due content at 03:15 UTC and 14:15 UTC. It adds only content whose `publish_at` timestamp has been reached. Pinterest can then import the feed from:

`https://leanovich.github.io/leo-bergmann-books/feed.xml`

Before connecting the feed, claim the website in Pinterest. Every feed item links to the claimed website and the website links to the Amazon book.

## Security

- No account passwords, tokens, customer data, or private catalog files belong in this repository.
- The site uses no cookies and no external analytics.
- Internal campaign state, budgets, credentials, and operational notes must never be rendered on the public website or RSS feed.
