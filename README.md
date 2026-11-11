# oauth-pages

Static GitHub Pages site (served from `docs/`) that hosts the public pages required for Google OAuth / Google Auth Platform app verification.

## Contents

- `docs/googlec34e7d9a736db11f.html` — Google Search Console site-verification file. Must stay exactly as issued by Google.
- `docs/rent-tracker/` — homepage (`index.html`) and privacy policy (`privacy.html`) for the Rent Tracker app, a private, internal tool for a small group of authorized users.

The page URLs are registered in the Google Auth Platform consent screen, so don't rename or move them.

## Development

There is no build system or dependencies; the files are plain HTML published as-is. Preview locally with:

```
python3 -m http.server -d docs
```

Deploys happen by pushing to `main`.
