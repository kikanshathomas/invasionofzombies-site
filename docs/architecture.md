# Architecture

A browser asks GitHub Pages for a path. Pages runs Jekyll on `main` and returns the copied file. There is no application server, no database, and no API.

Jekyll is configured in `_config.yml` to copy files as they are (`theme: null`, no front matter on the pages). The HTML files are the whole program: each page carries its own CSS and the small scripts it needs. Shared bytes are the font files, the images, and `assets/js/qrcode.min.js`.

```
browser
  -> invasionofzombies.com (GitHub Pages, HTTPS, CNAME)
       -> index.html | download.html | privacy.html | 404.html
       -> /assets/fonts, /assets/img, /assets/js/qrcode.min.js
       -> outbound: Play listing, GoatCounter, Ko-fi, ubersoft.pro, mailto
```

`404.html` is not linked in the nav. Pages uses the filename when nothing else matches. `sitemap.xml` lists only `/`, `/download.html`, and `/privacy.html`. `robots.txt` allows the whole site and names that sitemap.

## What the pages load

On this domain: Outfit (woff2), icons, `og.png`, screenshots, the Play badge, and on the download page `qrcode.min.js`. The home page's lightbox shows the 2x WebP (`data-full`), not a separate asset.

Off this domain, one script: GoatCounter at `//gc.zgo.at/count.js`, with `data-goatcounter="https://invasionofzombies.goatcounter.com/count"`, on all four pages. `privacy.html` sections 03 and 06 describe it and say it is the only file loaded from outside this domain. An extra CDN script would make that sentence false.

Other outbound links, not scripts: the Play listing, `https://ko-fi.com/ubersoft` ("Support Development"), `https://ubersoft.pro`, and `mailto:support@ubersoft.pro`.

The download page builds the QR in the browser. If `qrcode.min.js` does not load, the script replaces the code with a plain text Play link. The header comment in that file records why it is vendored.

## Checked and kept

These were traced from the HTML, the sitemap, `CNAME`, and the live Play listing. They stay.

- Every file under `assets/`, plus the three icon files at the repo root. Each one is referenced.
- `qrcode.min.js`. The download page loads it.
- The GoatCounter snippet. The privacy policy names it, and it is on the live pages.
- `CNAME`, `robots.txt`, `sitemap.xml`, `404.html`.
- The class `donate` on the Ko-fi links. No CSS rule uses it, so it does not change how the link looks. It is live markup, so it was left.
- `id="top"` on the home header and `id="get"` on the home download band. Nothing in the repo links to them. Removing an id can break a saved URL, so they stay.
- The Apple App Store sentences in `privacy.html` (section 06 and the footer trademark line). The site and the Play listing only offer Android. The packaging repo depends on `@capacitor/ios` and has no `ios/` project. The policy text is visible legal copy, so this pass did not edit it.

Removed in the same pass as these docs, because a full-text search found no use: the home page's review-card CSS and the script that filled `[data-stars]` and `.av[data-name]`; unused home-page rules `.cta-row`, `.btn`, `.btn-primary`, `.btn-ghost`, `.dl-note`, and `.accent`; and the unused `.legal .note` rule on the privacy page. No page, asset, or backup file was unused.
