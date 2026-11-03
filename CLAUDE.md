# security-news

Pipeline behind the raqmana.ly news pages: `fetch_news.py` → `site/news.json` → GitHub Pages, hourly via `.github/workflows/update.yml`. See README.md for usage.

## Rules

### Copyright
- Store only the headline, source name, date, link, and an excerpt of at most 30 words from the feed's own summary.
- Never store full text or images, never scrape article pages, and never rewrite or summarise articles with AI.
- Every item credits and links to its source.

### Security
- Accept only `http:`/`https:` links (`safe_url`); drop the item otherwise.
- Strip HTML with a real parser.
- Never publish data carrying a `_fixture` key. The workflow checks for it.

### GitHub Actions
- Use least-privilege `permissions:`: the build job has `contents: read`; only the deploy job has `pages: write` and `id-token: write`.
- Pin every action to a full commit SHA, with a version comment.
- Keep the `concurrency` group.

### Simplicity
- Python 3 with `feedparser` and `requests` only, all versions pinned in `requirements.txt`.
- Run the tests (`python -m pytest`) before every commit.

### Sources
- Don't add or enable a source without the owner's OK.
- Proposed but not enabled:
  - Cybercast (Arabic)
  - AITNews (Arabic)
  - Google News search feeds for Libya + cyber terms (English and Arabic). They reach Libyan outlets without feeds
    (The Libya Observer, Al Wasat), but links go through Google redirects and Google's terms for these feeds are
    aimed at personal use. The owner has not decided.
- Partner feeds checked 2026-11-03 and left out: SolarWinds, Matrix42, SealPath, DataPatrol, dPhish (product
  marketing), Thinkst Canary (rarely posts); no feed at all: CyberVergent, WhiteGuard, Cyber Crucible, Forcepoint,
  Segura, Albaraka Insurance (not security news).
