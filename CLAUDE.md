# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

Static GitHub Pages site (served from `docs/`) that hosts the public pages required for Google OAuth / Google Auth Platform app verification. There is no build system, package manager, linter, or test suite — files are plain hand-written HTML published as-is.

## Public repository — security rules

This repository is PUBLIC. Everything committed (files, commit messages, PR descriptions, and git history) is visible to anyone. Never add or commit:

- Secrets or credentials: OAuth client IDs/secrets, API keys, tokens, passwords, private keys, `.env` files.
- Infrastructure details: real hostnames, URLs, IPs, or ports of the apps themselves, Google Cloud project IDs/numbers, internal service names, or anything describing how the apps are hosted or secured.
- Personal or employer information: personal/work email addresses, phone numbers, home paths, or employer names. Commits must use the personal Gmail address, not a work address.
- Details that help an attacker, such as who the authorized users are, how access control is configured, or known weaknesses.

If a task seems to require any of the above, stop and ask the user instead of writing it to a file. Keep page wording generic (e.g. "the developer contact listed in the associated Google Cloud project"). Before committing, review `git diff` for anything sensitive. If something sensitive was already committed, tell the user; deleting it in a new commit does not remove it from history.

## Layout

- `docs/googlec34e7d9a736db11f.html` — Google Search Console site-verification file. Its name and content must stay exactly as issued by Google; do not rename, reformat, or delete it.
- `docs/<app-name>/index.html` and `docs/<app-name>/privacy.html` — homepage and privacy policy for each OAuth app (currently only `rent-tracker`). These URLs are what get registered in the Google Auth Platform consent screen, so changing paths breaks the registered app config.

## Conventions

- Each app gets its own directory under `docs/` with an `index.html` that links to a relative `privacy.html`.
- Pages are minimal, dependency-free HTML (no CSS/JS, `lang="en"`, charset + viewport meta).
- Update the "Last updated" date in a privacy policy when its text changes.
- The apps are described as private, internal tools for a small group of authorized users; keep new page wording consistent with that.
- Deploys happen by pushing to `main`; preview locally with e.g. `python3 -m http.server -d docs`.
