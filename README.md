# Project Ragnarok — Closed Alpha Portal

This repository currently contains the playtest landing page only. The Godot game build will be uploaded as a GitHub Release after the next approved Codex build.

## Website

- `index.html` is a standalone static landing page.
- The code word is `awesome`.
- The download button is intentionally disabled until a tested release is available.
- The code-word gate is **not secure authentication**: anyone with access to the website source can find the word, and public release assets can be downloaded directly.

## Publishing

GitHub Pages is **not enabled by committing files**. Configure Pages in repository Settings → Pages when ready. The repository is currently private; GitHub Pages availability and public visibility depend on account/plan and repository settings. Do not make the repository public without deciding whether its contents should be public.

## Next playtest release

Have Codex export a Windows release build, test the standalone executable and save data, package it as a ZIP, then create a versioned GitHub Release. Update `index.html` with the approved release download URL and feedback instructions. Do not commit the Godot source or secrets as part of the release process.
