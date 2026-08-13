# GF43

Shared website for all GF43 applications, published with GitHub Pages.

- Home: <https://garbage-factory-43.github.io/>
- app-ads.txt: <https://garbage-factory-43.github.io/app-ads.txt>
- Privacy Policy — Ghi Điểm Bài: <https://garbage-factory-43.github.io/apps/ghi-diem-bai/privacy.html>
- Privacy Policy — Undercover: <https://garbage-factory-43.github.io/apps/undercover/privacy.html>
- Privacy Policy — Tic Tac Toe: <https://garbage-factory-43.github.io/apps/tic-tac-toe/privacy.html>

## Structure

```
/
├── index.html                        # home page, list of apps
├── styles.css                        # shared styles for every page
├── app-ads.txt                       # shared by all apps
├── .nojekyll                         # disable Jekyll, serve files as-is
├── .gitattributes                    # force LF line endings
└── apps/
    └── <app-slug>/
        └── privacy.html              # per-app privacy policy
```

Conventions:

- Every app gets its own folder under `apps/`. Use a lowercase, ASCII, hyphenated slug (e.g. `ghi-diem-bai`).
- All pages link to `/styles.css` using an absolute path starting with `/`.
- Never put a privacy policy at the root — it always lives in `apps/<app-slug>/`.

## Adding a new app

1. Create `apps/<app-slug>/`.
2. Copy `apps/ghi-diem-bai/privacy.html` as a template, then update the app name, effective date, and the sections describing the data and third-party services that app actually uses.
3. Add an `<article class="card">` block for the app to `index.html`.
4. If the app uses a new ad network or publisher, add the matching line to `app-ads.txt`. If it stays on the same AdMob account, no change is needed — one `app-ads.txt` serves every app under the same publisher.
5. Commit and push to `main`. GitHub Pages redeploys in about 1–2 minutes.

## Google Play Console settings

For each app, under **Store listing**:

| Field | Value |
| --- | --- |
| Developer website | `https://garbage-factory-43.github.io/` |
| Privacy policy | `https://garbage-factory-43.github.io/apps/<app-slug>/privacy.html` |
| Support email | the shared GF43 support address |

The developer website and support email are shared across all apps; only the privacy policy URL is per-app.

## Local preview

Serve over HTTP instead of opening the files directly with `file://`, because pages reference the absolute path `/styles.css`:

```bash
python -m http.server 8000
# then open http://localhost:8000
```

## Deployment

This is an organization GitHub Pages repository (`<org>.github.io`), so the contents of `main` are the website. There is no build step — pushing is deploying.

Configure it under **Settings → Pages → Source = Deploy from a branch**, branch `main`, folder `/ (root)`.
