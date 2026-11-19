# invasionofzombies-site

Public marketing site for Invasion Of Zombies at <https://invasionofzombies.com>.

This repository is the site only: four hand-written HTML pages, images, a self-hosted font, and one vendored script. The game is not built here. GitHub Pages publishes the `main` branch with Jekyll, and Jekyll copies the pages through unchanged. Merging to `main` is a publish.

Longer notes live in [`docs/`](docs/). `README.md` and `docs/` are listed in [`_config.yml`](_config.yml) so they are not copied onto the public site. There is no API and no changelog in this repo (QA & Security owns changelogs, and none has been added here).

## Page map

| Path | What it is |
|---|---|
| `index.html` | Home: features, five screenshots with a lightbox, benefits, FAQ, Google Play badge |
| `download.html` | Play badge plus a QR code that opens the Play listing on a phone |
| `privacy.html` | Privacy policy. Effective date 25 September 2026. This is the URL on the Play listing |
| `404.html` | Not-found page. GitHub Pages serves it for unknown URLs. `noindex`, not in the sitemap |
| `sitemap.xml` | `/`, `/download.html`, `/privacy.html` |
| `robots.txt` | Allows all crawlers and points at the sitemap |
| `CNAME` | `invasionofzombies.com` |
| `favicon.ico`, `favicon-32x32.png`, `apple-touch-icon.png` | 16/32/48 icon, 32px PNG, 180px Apple touch icon. Linked from every page |
| `assets/img/og.png` | 1024×500 share image. The home, download, and privacy heads declare that size. The home-page comment says this file is also the Play feature graphic |
| `assets/img/app-icon.png` | 208×208 icon, shown at 96px on the home page and 104px on the download page |
| `assets/img/google-play-badge.png` | Official badge image (478×142), displayed at 54px or 56px tall |
| `assets/img/shots/` | Five screenshots. Each is a 460×818 JPEG plus a 920×1636 WebP used for the 2x source and the lightbox |
| `assets/fonts/` | Outfit woff2 at weights 400, 500, 600, and 700. Weight 300 on the home page uses the 400 file |
| `assets/js/qrcode.min.js` | Vendored [qrcodejs](https://github.com/davidshimjs/qrcodejs) (MIT). Used only by `download.html` |

The Play links all use `https://play.google.com/store/apps/details?id=com.invasionofzombies.app`.

## How it is published

GitHub Pages, legacy Jekyll build, from branch `main`, folder `/`. The custom domain in `CNAME` is `invasionofzombies.com`, and HTTPS is enforced. There is no GitHub Actions workflow and no build step of our own.

[`_config.yml`](_config.yml) does three jobs:

- `theme: null`, so Pages does not inject its default theme stylesheet.
- `require_front_matter: true`, so a markdown file without front matter is copied as the raw file rather than turned into HTML. The HTML pages have no front matter and are copied byte for byte.
- `exclude` keeps `CLAUDE.md`, `.claude`, `README.md`, `readme.md`, and `docs` off the site. Files that start with `.` or `_` (`.gitattributes`, `_config.yml`) are already skipped by Jekyll.

Do not add YAML front matter to a page. That would make Jekyll render it instead of copying it.

Company rule, same as the other live sites: a merge to `main` waits for a DevOps security check, QA review, a clearance line in `kikanshathomas/ubersoft-company` `company/audit/cleared.md`, and Thomas's go. QA owns any changelog. This PR does not add one.

## How to edit and preview

Edit the HTML. Styles and the small scripts are inside each page, except `assets/js/qrcode.min.js`.

Root-absolute paths (`/assets/...`, `/privacy.html`) only work when the site root is the server root. From this directory:

```sh
python3 -m http.server 8000
```

Then open <http://127.0.0.1:8000/>, <http://127.0.0.1:8000/download.html>, and <http://127.0.0.1:8000/privacy.html>. Opening an HTML file directly (`file://`) will not load the font, icons, or screenshots.

There is no `package.json`. Nothing here is compiled.

When a public URL is added or removed, update `sitemap.xml` in the same change. The four pages above are the whole public set. Leave `privacy.html` at `/privacy.html`: the Play listing links to `https://invasionofzombies.com/privacy.html`, and its support contact is `mailto:support@ubersoft.pro`. The site footer uses that same address. There is no support page to rename.

A wording change in `privacy.html` has to update the effective date in that file (the `<time datetime>` and the visible date). The only script loaded from another domain is GoatCounter (`//gc.zgo.at/count.js`), which the policy names in sections 03 and 06. Fonts, images, and `qrcode.min.js` stay on this domain.

## Related repositories

| Repo | Role |
|---|---|
| [`kikanshathomas/invasionofzombies`](https://github.com/kikanshathomas/invasionofzombies) | Android package. Capacitor app id `com.invasionofzombies.app`, `android/`, `capacitor.config.json`. The game's web build is `www/` in that repo (Capacitor reads `dist/`). This site does not import it |
| [`kikanshathomas/invasionofzombies-dev`](https://github.com/kikanshathomas/invasionofzombies-dev) | Empty. Other Ubersoft products keep source in `-dev`. This one does not, yet |

Play listing checked 19 November 2026: website `https://invasionofzombies.com`, privacy policy `https://invasionofzombies.com/privacy.html`, support email `support@ubersoft.pro`.

## Docs

| File | Contents |
|---|---|
| [docs/overview.md](docs/overview.md) | What the site is for, and who changes it |
| [docs/architecture.md](docs/architecture.md) | How a request is served, and what was checked and kept |
| [docs/setup.md](docs/setup.md) | Local preview |
| [docs/deploy.md](docs/deploy.md) | Pages settings and the URLs that must keep working |
