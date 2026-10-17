# Gnomod

Custom Dalamud plugin repository for gnomerock's FFXIV plugins.

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
| **Konnyaku Jelly** | Translates FFXIV chat between English and Japanese with ChatGPT, Claude or Gemini. [Tutorial](https://gnomerock.github.io/konyakku/) | [gnomerock/konyakku](https://github.com/gnomerock/konyakku) |

## How it works

`repo.json` lists every plugin. Each plugin lives in its own repo and publishes `latest.zip` on its own GitHub Releases page. Its release workflow then updates only its own entry here (matched by `InternalName`), using a `GNOMOD_TOKEN` secret that can write to this repo.

To add a plugin:
1. Add an entry to `repo.json` with a unique `InternalName`.
2. Copy the release workflow from `gnomerock/konyakku` into the plugin's repo and change `PLUGIN` to its `InternalName`.
3. Add the `GNOMOD_TOKEN` secret to the plugin's repo.
