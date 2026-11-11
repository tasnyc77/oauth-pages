# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

Static GitHub Pages site (served from `docs/`) that hosts the public pages required for Google OAuth / Google Auth Platform app verification. There is no build system, package manager, linter, or test suite — files are plain hand-written HTML published as-is.

## Layout

- `docs/googlec34e7d9a736db11f.html` — Google Search Console site-verification file. Its name and content must stay exactly as issued by Google; do not rename, reformat, or delete it.
- `docs/<app-name>/index.html` and `docs/<app-name>/privacy.html` — homepage and privacy policy for each OAuth app (currently only `rent-tracker`). These URLs are what get registered in the Google Auth Platform consent screen, so changing paths breaks the registered app config.

## Conventions

- Each app gets its own directory under `docs/` with an `index.html` that links to a relative `privacy.html`.
- Pages are minimal, dependency-free HTML (no CSS/JS, `lang="en"`, charset + viewport meta).
- Update the "Last updated" date in a privacy policy when its text changes.
- The apps are described as private, internal tools for a small group of authorized users; keep new page wording consistent with that.
- Deploys happen by pushing to `main`; preview locally with e.g. `python3 -m http.server -d docs`.
