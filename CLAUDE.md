# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

`waterplane-dev/media`: walkthrough videos for waterplane, hosted outside the main repo's history (too big for every clone). No code, no build, no tests. It is served by GitHub Pages at `https://waterplane-dev.github.io/media/<name>` (`.nojekyll` keeps Pages from processing it); `https://cdn.jsdelivr.net/gh/waterplane-dev/media@main/<name>` serves the same files.

## How files get here

Nothing in this repo is edited by hand. The source repo (`../usmc`) owns it:

- Source videos live in usmc at `docs/media/*.mp4`; `deploy/public-media.json` there lists what is hosted.
- `scripts/release/publish-public.mjs --media-to ../waterplane-media` renames each file to `<stem>-<sha256:10>.<ext>` (first 10 hex chars of the file's SHA-256), copies it here, re-points every published markdown link at this URL, and commits as `Media for waterplane <version>`. In usmc this runs via the public-snapshot build in `.waterplane-shared/builds.json`, which also pushes this repo before the public repo.
- A re-recording gets a new hash, so a new name; older releases keep their links. Never rename, overwrite or delete a published file: `waterplane-public/README.md`, `docs/guide.md` and past releases link to the exact names.

The publish script refuses to run if this clone has uncommitted changes (`git status --porcelain` non-empty) and commits with `git add --all`, so anything left lying around here either blocks the publish or gets swept into the media commit.

## waterplane phone transport

Artifacts meant for the phone go in `.claude/outbox/`; uploads from the phone arrive in `.claude/inbox/`. Both are gitignored — never commit them.
