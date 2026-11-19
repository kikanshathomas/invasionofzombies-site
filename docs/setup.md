# Setup

No install. No Node, Ruby, or bundler is required to edit or preview the pages.

From the repository root:

```sh
python3 -m http.server 8000
```

Open:

- <http://127.0.0.1:8000/>
- <http://127.0.0.1:8000/download.html>
- <http://127.0.0.1:8000/privacy.html>
- <http://127.0.0.1:8000/no-such-page> to see `404.html` only if the server falls back to it. Python's `http.server` does not. GitHub Pages does, because the file is named `404.html`.

Use a server. The pages refer to `/assets/...` and `/favicon.ico`. A `file://` open leaves those requests at the disk root, so fonts and images fail.

What to click when checking a change:

- Home: menu at a narrow width, a screenshot (lightbox, then Escape), an FAQ row, both Play badges.
- Download: the QR draws inside the white card, and the badge opens Play.
- Privacy: the effective date still matches the `<time datetime>`.

`README.md` and `docs/` are for people reading the repo. They are excluded in `_config.yml` and are not part of the preview of the public site. See [deploy.md](deploy.md).
