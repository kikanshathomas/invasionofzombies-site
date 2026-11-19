# Deploy

Publishing is GitHub Pages on the `main` branch, source path `/`, build type legacy (Jekyll). Confirmed from the repository's Pages settings: custom domain `invasionofzombies.com`, HTTPS enforced, public. `CNAME` in the repo is the same domain. There is no workflow file under `.github/`.

A push or merge to `main` is what Pages builds. Company rules still apply: DevOps security review, QA review, a line in `kikanshathomas/ubersoft-company` `company/audit/cleared.md`, and Thomas's go before that merge. This repo has no deploy script of its own.

## What Jekyll copies

`_config.yml` sets `theme: null` and `require_front_matter: true`. Pages without front matter are copied unchanged. That is why the live HTML matches the files in git.

Excluded, so they must not become public URLs:

- `CLAUDE.md` and `.claude` (already excluded; `https://invasionofzombies.com/CLAUDE.md` is a 404)
- `README.md` and `readme.md`
- `docs`

Jekyll also skips names that start with `.` or `_`, which covers `.gitattributes` and `_config.yml`. `https://invasionofzombies.com/.gitattributes` is a 404.

After this change is on `main`, these should stay 404s:

- `https://invasionofzombies.com/README.md`
- `https://invasionofzombies.com/readme.md`
- `https://invasionofzombies.com/docs/overview.md`

A sibling marketing site that does not exclude its readme does serve it (`https://zbilltracker.com/readme.md`). The exclude list is what prevents that here. Do not remove those entries.

## URLs that must keep working

Checked against the files and the Play listing for `com.invasionofzombies.app` on 19 November 2026:

| URL | Who uses it |
|---|---|
| `https://invasionofzombies.com/` | Play listing website link. `CNAME`, sitemap |
| `https://invasionofzombies.com/privacy.html` | Play listing privacy-policy link. Footer on every page. Sitemap |
| `https://invasionofzombies.com/download.html` | Home nav "Get the app". Sitemap |
| `mailto:support@ubersoft.pro` | Play listing support email. Footer "Support" and privacy section 12 |
| `https://play.google.com/store/apps/details?id=com.invasionofzombies.app` | Every Play badge and the QR code |

Do not rename `privacy.html`, do not drop it from the sitemap, and do not change `CNAME` in a docs-only change.

Pages can take a few minutes, and the CDN caches responses (the live pages send `cache-control: max-age=600`). To see what visitors get:

```sh
curl -sI "https://invasionofzombies.com/privacy.html?v=$(date +%s)"
curl -s "https://invasionofzombies.com/privacy.html?v=$(date +%s)" | grep -o 'Effective date: <time[^>]*>[^<]*'
```

Call a change live only when the served HTML matches the file that was merged.
