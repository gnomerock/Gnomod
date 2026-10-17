# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

Gnomod is gnomerock's custom Dalamud (FFXIV) plugin repository. It has no plugin source code, no build step and no tests. It contains:

- `repo.json`: the Dalamud plugin manifest that users add in-game as a custom repository (`https://raw.githubusercontent.com/gnomerock/Gnomod/main/repo.json`). It is a JSON array with one object per plugin.
- `index.html`: a single-file static site (inline CSS/JS, no framework) served by GitHub Pages from the root of `main` at https://gnomerock.github.io/Gnomod/.
- `icon.png`: the Gnomod icon, used by the site and README.

## How plugins get here

Each plugin lives in its own repo (e.g. `gnomerock/konnyaku-jelly`) and publishes `latest.zip` on its GitHub Releases. That repo's release workflow writes back to `repo.json` here, updating only the entry whose `InternalName` matches its `PLUGIN` setting, using a `GNOMOD_TOKEN` secret. So version fields (`AssemblyVersion`, `DownloadLink*`, `LastUpdate`) are normally changed by CI, not by hand. Commits like "Update Konyakku to x.y.z" come from that workflow.

To add a plugin:
1. Add an entry to `repo.json` with a unique `InternalName` (it must match the plugin assembly's internal name; e.g. Konnyaku Jelly's is `Konyakku`).
2. Copy the release workflow from `gnomerock/konnyaku-jelly` into the plugin's repo and set `PLUGIN` to its `InternalName`.
3. Add the `GNOMOD_TOKEN` secret to the plugin's repo.
4. Add a row to the Plugins table in `README.md`.

Keep `repo.json` valid JSON with the existing field set and 2-space indentation, because both Dalamud and the release workflows parse it.

## The website (`index.html`)

- It fetches `repo.json` at page load and renders it, so new plugins and versions need no page edits.
- Download counts come from the GitHub Releases API for each plugin's `RepoUrl`. This is optional, and the page works if it fails.
- Things `repo.json` has no field for are set in the script: `EXTRAS` (keyed by `InternalName`, e.g. a `guide` tutorial link that shows a "How to use" button) and `HIDDEN_TAGS` (tags left out of the filter row).
- Theming uses CSS custom properties on `:root`, with dark-mode overrides under both `prefers-color-scheme: dark` and `:root[data-theme="dark"]`. Change both blocks together.
- Values from `repo.json` are inserted with the `esc()`/`safeUrl()` helpers. Keep using them for any new fields.

To preview locally, serve the folder over HTTP, since `fetch('repo.json')` fails under `file://`:

```
python -m http.server 8000
```
