# Meal Planner: for developers

Everything technical about this project. The [README](../README.md) is for everyone else.

[![Checks](https://github.com/RandomFab/meal-planner/actions/workflows/ci.yml/badge.svg)](https://github.com/RandomFab/meal-planner/actions/workflows/ci.yml)
[![Release](https://img.shields.io/github/v/release/RandomFab/meal-planner?include_prereleases)](https://github.com/RandomFab/meal-planner/releases)
[![License: MIT](https://img.shields.io/badge/license-MIT-blue)](../LICENSE)

## What it is

A single [Agent Skill](https://docs.claude.com/en/docs/agents-and-tools/agent-skills/overview) that plans a household's meals in a Notion workspace, through the Notion connector. The repository is also a Claude Code plugin.

- No code runs: the skill is instructions only (Markdown).
- Data lives in the user's copy of the [Notion template](https://garrulous-amount-bc1.notion.site/Meal-Planner-Template-40fd46912afe81f2b234f62e9acec937). Nothing is stored anywhere else.
- It needs the Notion connector (claude.ai) or the Notion MCP server (Claude Code).

## Install in Claude Code

```text
/plugin marketplace add RandomFab/claude-plugins
/plugin install meal-planner@randomfab
```

Then connect Notion (`/mcp`) and share your Meal Planner page with it.

A plugin installed from claude.ai (**Plugins → Add → Add marketplace**, `RandomFab/claude-plugins`) is saved to the account: it also reaches Cowork, scheduled tasks and Claude Code (as a synced plugin) without a second install. The release asset `meal-planner.zip` is the plugin itself (`.claude-plugin/plugin.json` + `skills/`), for **Add → Upload plugin**.

To try a local copy instead, clone this repository and run `/plugin marketplace add ./` from a folder that holds a `marketplace.json` pointing to it, or copy `skills/meal-planner/` into `~/.claude/skills/`.

## Layout

```text
meal-planner/
├── .claude-plugin/plugin.json     # name, version (single source of truth), metadata
├── skills/meal-planner/
│   ├── SKILL.md                   # entry point: rules, routing table, help list
│   └── references/                # loaded on demand
│       ├── notion-schema.md       # finding the workspace, every database and property, read/write rules
│       ├── setup.md               # guided setup, settings, modules
│       ├── recipe.md              # adding and fixing dishes
│       ├── plan-week.md           # weekly menu
│       ├── shopping.md            # shopping list (computed by Notion)
│       ├── stock.md               # what is at home: counts and corrections
│       ├── daily-brief.md         # today's meals, scheduled brief
│       └── feedback.md            # what was eaten, feedback, plan changes, preferences
├── examples/                      # fictional household and sample exchanges
├── docs/                          # this file, banners, media
└── .github/                       # checks, release, issue templates
```

`SKILL.md` stays short and routes each request to one reference. A reference is read only when its task comes up, which keeps the context small.

## Notion data model

Four databases under a root page, plus a **Household profile** page that holds every setting and what Claude has learned, and a **Shopping list** page that shows a view of Products. Full schema in [`notion-schema.md`](../skills/meal-planner/references/notion-schema.md).

| Database | One row per | Key relations |
| --- | --- | --- |
| Menu | meal (date × lunch/dinner) | Dish |
| Dishes | dish, steps in the page body | Dish ingredients, Menu |
| Dish ingredients | ingredient of a dish, for one adult portion | Dish, Product |
| Products | product bought, its stock and what to buy | Used in |

Design choices:

- **Notion computes what is deterministic, Claude does the rest.** The shopping list and the stock are formulas, always up to date: Claude never writes them. Claude plans, writes recipes, and records counts and corrections in the user's words.
- **Stock is a ledger, not a level.** `Stock = Stock count + Bought since − Eaten since`. Eating is derived from the menu (Cooked meals, and Planned meals in the past), buying from the Bought button, so nobody updates the stock by hand. A count resets it.
- **Quantities for one adult portion**, scaled by each member's appetite (adult 1, light 0.8, child 0.5).
- **Rollups and formulas are display-only**: the connector can't read them, so the skill reads views (the "To buy" view gives the list) or computes from the base properties.
- **Reads avoid SQL**: outside Notion's Business plan, SQL queries share a small quota. The skill reads saved views first, then filtered rows, and SQL only as a last resort.
- **Propose before writing**: every change is shown and approved, except what the user's own message asks for (a count, an item to add).
- **Never delete**: statuses (Banned, Skipped, Postponed) instead. The only exception is removing the template's sample dishes during setup, on request.

The template version is stored in the profile page. A change to database or property names is a major version (users must duplicate a new template).

### Products formulas

The Notion API can't create a formula that reads related pages, so the first three are pasted in the Notion editor when building the template. Users get them by duplicating it.

| Property | Formula |
| --- | --- |
| Need 7d | `prop("Used in").map(lets(q, current.prop("Quantity"), s, current.prop("Dish").map(current.prop("Menu")).flat().filter(current.prop("Status") == "Planned" and dateBetween(current.prop("Date"), today(), "days") >= 0 and dateBetween(current.prop("Date"), today(), "days") <= 7).map(current.prop("Servings")).sum(), q * s)).sum()` |
| Eaten since | `lets(d, if(empty(prop("Counted on")), parseDate("<template date>"), prop("Counted on")), prop("Used in").map(lets(q, current.prop("Quantity"), s, current.prop("Dish").map(current.prop("Menu")).flat().filter(dateBetween(current.prop("Date"), d, "days") >= 0 and (current.prop("Status") == "Cooked" or (current.prop("Status") == "Planned" and dateBetween(current.prop("Date"), today(), "days") < 0))).map(current.prop("Servings")).sum(), q * s)).sum())` |
| For dishes | `prop("Used in").filter(current.prop("Dish").map(current.prop("Menu")).flat().filter(current.prop("Status") == "Planned" and dateBetween(current.prop("Date"), today(), "days") >= 0 and dateBetween(current.prop("Date"), today(), "days") <= 7).length() > 0).map(current.prop("Dish").first().prop("Name")).unique().join(", ")` |
| Stock | `if(prop("Staple"), 0, max(round((if(empty(prop("Stock count")), 0, prop("Stock count")) + if(empty(prop("Bought since")), 0, prop("Bought since")) - prop("Eaten since")) * 100) / 100, 0))` |
| Buy qty | `lets(per, prop("Recipe units per pack"), missing, round((prop("Need 7d") - prop("Stock")) * 100) / 100, if(prop("Staple") or missing <= 0, 0, if(empty(per) or per <= 0, ceil(missing), ceil(missing / per) * per)))` |
| To buy | `lets(per, prop("Recipe units per pack"), q, prop("Buy qty"), unit, format(prop("Recipe unit")), pack, if(empty(prop("Pack size")), "pack", prop("Pack size")), if(q > 0, if(empty(per) or per <= 0, format(q) + if(unit == "piece" or unit == "", "", " " + unit), format(round(q / per)) + " × " + pack), if(prop("Add to list"), "1 × " + pack, "")))` |

The **Bought** button has two actions: edit Bought since to `Bought since + Buy qty` (on this page), and untick Add to list.

## Releases

Version lives in `.claude-plugin/plugin.json` only. Work happens on `develop`; `main` only receives releases.

1. Update `version` in `plugin.json`, move `Unreleased` in `CHANGELOG.md` to a dated section.
2. Commit `release: vX.Y.Z`, merge `develop` into `main`.
3. Tag `main`: `git tag -a vX.Y.Z -m "vX.Y.Z"`, push `main` and the tag.
4. The `Release` workflow checks the tag against `plugin.json`, zips the plugin (`.claude-plugin/`, `skills/`, `LICENSE`), and creates the GitHub release with the CHANGELOG section as notes. Tags with a `-` (betas) are marked as pre-releases.

The `Checks` workflow runs on every push: `plugin.json` version, skill frontmatter, required files, a CHANGELOG entry for the current version, no file of 5 MiB or more, no system files, and a secret scan.

## Contributing

Bug reports and ideas are welcome through [issues](https://github.com/RandomFab/meal-planner/issues). For a change to the instructions, open an issue first: describe what you asked Claude, what it did, and what it should have done.

When editing the skill:

- Write in English; the skill answers in the user's language.
- Keep `SKILL.md` under 500 lines and references one level deep.
- Use fictional data only, in examples and anywhere else.
- Update both READMEs together when a user-facing behaviour changes, and add a line to `Unreleased` in the CHANGELOG.

## License

[MIT](../LICENSE) © Fabien Bardouil
