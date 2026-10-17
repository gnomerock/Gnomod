# Gnomod

<img src="icon.png" alt="Gnomod" width="96" align="right">

Custom Dalamud plugin repository for gnomerock's FFXIV plugins.

**🛒 Browse the plugins: https://gnomerock.github.io/Gnomod/**

## Install

1. In game, type `/xlsettings` → **Experimental** tab.
2. Under **Custom Plugin Repositories**, paste:
   ```
   https://raw.githubusercontent.com/gnomerock/Gnomod/main/repo.json
   ```
   tick **Enabled**, click **+**, then **Save and Close**.
3. Type `/xlplugins` → **All Plugins** and install any of the plugins below.

## Plugins

| Plugin | What it does | Source |
|---|---|---|
| **Konnyaku Jelly** | Translates FFXIV chat between English and Japanese with ChatGPT, Claude or Gemini. [Tutorial](https://gnomerock.github.io/konnyaku-jelly/) | [gnomerock/konnyaku-jelly](https://github.com/gnomerock/konnyaku-jelly) |
| **Tazunebito Stick** | Lists Party Finder listings in its own window and filters them with filters you save (duty, open slots for your job, item level, objective and more). | [gnomerock/tazunebito-stick](https://github.com/gnomerock/tazunebito-stick) |

## How it works

`repo.json` lists every plugin. Each plugin lives in its own repo and publishes `latest.zip` on its own GitHub Releases page. Its release workflow then updates only its own entry here (matched by `InternalName`), using a `GNOMOD_TOKEN` secret that can write to this repo.

To add a plugin:
1. Add an entry to `repo.json` with a unique `InternalName`.
2. Copy the release workflow from `gnomerock/konnyaku-jelly` into the plugin's repo and change `PLUGIN` to its `InternalName`.
3. Add the `GNOMOD_TOKEN` secret to the plugin's repo.

## Website

`index.html` is the plugin listing at https://gnomerock.github.io/Gnomod/ (GitHub Pages, served from the root of `main`). It reads `repo.json` when the page loads, so new plugins and versions show up there without editing the page. Download counts come from each plugin's GitHub releases. For a "How to use" button, add the plugin's tutorial link to `EXTRAS` in `index.html`. `icon.png` was generated with Codex CLI.
