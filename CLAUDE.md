# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository purpose

Japanese translation of the BentoBox documentation site (a Minecraft Bukkit plugin framework). The site is built with [Zensical](https://zensical.org) (the successor to Material for MkDocs; it reads the MkDocs-style `mkdocs.yml`) and published via Read the Docs. Almost all content is Markdown under `docs/`; the rest of the repo is the build configuration and a small set of macros that generate tables at build time.

## Common commands

Use the in-repo virtualenv (`.venv/`) or install requirements first:

```bash
pip install -r requirements.txt
zensical serve     # local preview at http://localhost:8000
zensical build     # output to ./site
```

Read the Docs uses Python 3.12 and runs `zensical build` (see `.readthedocs.yml`); `.github/workflows/zensical.yml` runs the same build on every push and PR. `requirements.txt` is kept as the MkDocs fallback (`pip install -r requirements.txt && mkdocs build`); Zensical does not support the `git-revision-date-localized` plugin, so the "last updated" line is not shown. There are no tests or linters.

## Architecture

- **`mkdocs.yml`** — site definition: navigation tree (in Japanese), Material theme config (`theme.language: ja`), enabled markdown extensions, and the `macros` plugin that loads `main.py`. The `nav:` section is the source of truth for site structure; new pages must be added there to appear.
- **`main.py`** — `mkdocs-macros-plugin` entry point. Defines `define_env(env)` and registers Jinja macros that pages call inline (e.g. `{{ translations(...) }}`, `{{ addon_description(...) }}`, `{{ placeholders_bundle(...) }}`, `{{ placeholders_source(...) }}`, `{{ flags_bundle(...) }}`, `{{ flags_source(...) }}`). These macros generate Markdown tables at build time by reading the CSVs in `data/`. The intro text and table headers inside the `translations()` macro are Japanese-translated in `main.py` itself — keep them intact when syncing from English.
- **`data/`** — source data for the macros: `flags.csv`, `placeholders.csv`, `permissions.csv`, and `minecraft-block-and-entity.json` (used by `icon_css()` to map a block/entity name to a CSS class for the Minecraft icon sprite sheet referenced in `docs/stylesheets/icons-minecraft-0.5.css`).
- **`docs/stylesheets/`** — Custom CSS loaded via `extra_css` in `mkdocs.yml`
  - `bentobox-theme.css` — Blueprint palette override for the Material slate scheme (navy/cyan; Space Grotesk + Inter Tight + JetBrains Mono). Also defines all `.bb-*` layout classes used exclusively by `docs/index.md`.
  - `icons-minecraft-0.5.css` — Minecraft block/entity icon sprites
- **`docs/`** — Japanese Markdown content, organised by section: `BentoBox/` (core docs), `gamemodes/`, `addons/`, `Tutorials/`, plus top-level `index.md`, `FAQ.md`, `Glossary.md`.

## Homepage (docs/index.md)

`index.md` is structurally different from all other pages. It uses `hide: [navigation, toc]` frontmatter and its body is a single raw HTML block (no Markdown) built from `.bb-*` CSS classes defined in `bentobox-theme.css`. Do not add Markdown content or macros directly inside the `.bb-homepage` wrapper — use plain HTML.

## Translation notes

- This repo is the Japanese (`ja`) variant — `theme.language: ja` and `plugins.search.lang: ja` in `mkdocs.yml`. UI strings, nav labels, and page content should all be in Japanese; code identifiers, macro names, CSV column keys, and file paths stay in English.
- The upstream English docs live at https://github.com/BentoBoxWorld/docs. When syncing new content from upstream, translate the prose but keep macro calls, front matter, links, and file names identical so cross-references and the macro system keep working.

## Dependency Source Lookup

When you need to inspect source code for a dependency (e.g., BentoBox, addons):

1. **Check local Maven repo first**: `~/.m2/repository/` — sources jars are named `*-sources.jar`
2. **Check the workspace**: Look for sibling directories or Git submodules that may contain the dependency as a local project (e.g., `../bentoBox`, `../addon-*`)
3. **Check Maven local cache for already-extracted sources** before downloading anything
4. Only download a jar or fetch from the internet if the above steps yield nothing useful

Prefer reading `.java` source files directly from a local Git clone over decompiling or extracting a jar.

In general, the latest version of BentoBox should be targeted.

## Project Layout

Related projects are checked out as siblings under `~/git/`:

**Core:**
- `bentobox/` — core BentoBox framework

**Game modes:**
- `addon-acidisland/` — AcidIsland game mode
- `addon-bskyblock/` — BSkyBlock game mode
- `Boxed/` — Boxed game mode (expandable box area)
- `CaveBlock/` — CaveBlock game mode
- `OneBlock/` — AOneBlock game mode
- `SkyGrid/` — SkyGrid game mode
- `RaftMode/` — Raft survival game mode
- `StrangerRealms/` — StrangerRealms game mode
- `Brix/` — plot game mode
- `parkour/` — Parkour game mode
- `poseidon/` — Poseidon game mode
- `gg/` — gg game mode

**Addons:**
- `addon-level/` — island level calculation
- `addon-challenges/` — challenges system
- `addon-welcomewarpsigns/` — warp signs
- `addon-limits/` — block/entity limits
- `addon-invSwitcher/` / `invSwitcher/` — inventory switcher
- `addon-biomes/` / `Biomes/` — biomes management
- `Bank/` — island bank
- `Border/` — world border for islands
- `Chat/` — island chat
- `CheckMeOut/` — island submission/voting
- `ControlPanel/` — game mode control panel
- `Converter/` — ASkyBlock to BSkyBlock converter
- `DimensionalTrees/` — dimension-specific trees
- `discordwebhook/` — Discord integration
- `Downloads/` — BentoBox downloads site
- `DragonFights/` — per-island ender dragon fights
- `ExtraMobs/` — additional mob spawning rules
- `FarmersDance/` — twerking crop growth
- `GravityFlux/` — gravity addon
- `Greenhouses-addon/` — greenhouse biomes
- `IslandFly/` — island flight permission
- `IslandRankup/` — island rankup system
- `Likes/` — island likes/dislikes
- `Limits/` — block/entity limits
- `lost-sheep/` — lost sheep adventure
- `MagicCobblestoneGenerator/` — custom cobblestone generator
- `PortalStart/` — portal-based island start
- `pp/` — pp addon
- `Regionerator/` — region management
- `Residence/` — residence addon
- `TopBlock/` — top ten for OneBlock
- `TwerkingForTrees/` — twerking tree growth
- `Upgrades/` — island upgrades (Vault)
- `Visit/` — island visiting
- `weblink/` — web link addon
- `CrowdBound/` — CrowdBound addon

**Data packs:**
- `BoxedDataPack/` — advancement datapack for Boxed

**Documentation & tools:**
- `docs/` — main English documentation site
- `docs-chinese/` — Chinese documentation
- `docs-french/` — French documentation
- `docs-japanese/` — Japanese documentation (this repo)
- `BentoBoxWorld.github.io/` — GitHub Pages site
- `website/` — website
- `translation-tool/` — translation tool

Check these for source before any network fetch.

## Key Dependencies (source locations)

- `world.bentobox:bentobox` → `~/git/bentobox/src/`
