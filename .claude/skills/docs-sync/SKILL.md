---
name: docs-sync
description: Audit README.md and CLAUDE.md (and the privacy-policy pages under docs/) for drift against the site contents, fix what is stale, and open a PR. Use when asked to sync, refresh or check the docs.
disable-model-invocation: true
allowed-tools: Bash(git *) Bash(gh *) Bash(ls *) Bash(find *) Read Edit Grep Glob
---

# docs-sync

Optional argument: a path (e.g. `docs/rent-tracker`) limiting the audit to that directory.
With no argument, audit everything. Arguments: $ARGUMENTS

## 1. Preconditions
- `git status --porcelain` must be empty and the branch must be `main`; otherwise stop and tell the user.
- `git pull --ff-only`.

## 2. Audit (read-only)
Compare each doc against its source of truth. Only flag real drift (wrong/missing/stale facts), not style.

| Doc | Check against |
|---|---|
| `README.md` | what is actually under `docs/` |
| `CLAUDE.md` | `docs/` layout (verification file, one directory per app with `index.html` + `privacy.html`), the conventions listed (relative `privacy.html` link, dependency-free HTML, `lang="en"`, charset + viewport meta, "Last updated" date), deploy/preview commands |

Look for: apps under `docs/` that are not documented (or documented but removed), renamed files/paths, a `Last updated` date that is older than the latest `git log` change to that privacy page, broken relative links, stale wording about who the apps are for.

Rules:
- Never edit, rename or reformat `docs/googlec34e7d9a736db11f.html` (Google Search Console verification file).
- Do not change page URLs/paths under `docs/<app>/`; they are registered in the Google Auth Platform consent screen. Flag such issues under "Needs human review".
- Do not change the wording of a privacy policy beyond fixing a stale "Last updated" date; policy text changes are for a human.
- No secrets or credentials in docs.

## 3. Fix
- Minimal, targeted edits only. No rewrites, reflowing or reformatting.
- If nothing drifted: report "docs are in sync", create no branch and no PR, and stop.
- Anything ambiguous (cannot tell whether the doc or the code is right): do not edit; list it in the report/PR body under "Needs human review".

## 4. Validate
This repo has no pre-commit config or build. Re-read each edited file and confirm relative links still resolve (`ls`/`find`).

## 5. Confirm, then PR
1. Show the user a per-file summary (what changed and why) and `git diff --stat`. Always include a `CLAUDE.md: in sync` or `CLAUDE.md: changed` line.
2. Ask for confirmation before any push. Do not push without a yes.
3. On yes:
   - `git switch -c docs/sync-$(date +%F)`
   - Commit with a concise message, ending with the attribution line from the session's system reminder.
   - `git push -u origin HEAD`
   - `gh pr create --base main` with a body listing each file changed and why, a "Needs human review" section if any, and the PR attribution line from the session's system reminder.
4. Print the PR URL.
