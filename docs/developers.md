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
/plugin install meal-planner@claude-plugins
```

Then connect Notion (`/mcp`) and share your Meal Planner page with it.

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
│       ├── shopping.md            # shopping list
│       ├── stock.md               # what is left at home (optional module)
│       ├── daily-brief.md         # today's meals, scheduled brief
│       └── feedback.md            # what was eaten, feedback, plan changes, preferences
├── examples/                      # fictional household and sample exchanges
├── docs/                          # this file, banners, media
└── .github/                       # checks, release, issue templates
```

`SKILL.md` stays short and routes each request to one reference. A reference is read only when its task comes up, which keeps the context small.

## Notion data model

Five databases under a root page, plus a **Household profile** page that holds every setting and what Claude has learned. Full schema in [`notion-schema.md`](../skills/meal-planner/references/notion-schema.md).

| Database | One row per | Key relations |
| --- | --- | --- |
| Menu | meal (date × lunch/dinner) | Dish |
| Dishes | dish, steps in the page body | Dish ingredients, Menu |
| Dish ingredients | ingredient of a dish, for one adult portion | Dish, Product |
| Products | product bought; stock level if tracking is on | Used in, Shopping list |
| Shopping list | product to buy for a week | Product |

Design choices:

- **Quantities for one adult portion**, scaled by each member's appetite (adult 1, light 0.8, child 0.5).
- **Rollups and formulas are display-only**: the connector can't read them, so the skill computes from the base properties.
- **Reads avoid SQL**: outside Notion's Business plan, SQL queries share a small quota. The skill reads saved views first, then filtered rows, and SQL only as a last resort.
- **Propose before writing**: every change is shown and approved, except steps the user authorised in advance (stock updates once tracking is on).
- **Never delete**: statuses (Banned, Skipped, Postponed) instead. The only exception is removing the template's sample dishes during setup, on request.

The template version is stored in the profile page. A change to database or property names is a major version (users must duplicate a new template).

## Releases

Version lives in `.claude-plugin/plugin.json` only. Work happens on `develop`; `main` only receives releases.

1. Update `version` in `plugin.json`, move `Unreleased` in `CHANGELOG.md` to a dated section.
2. Commit `release: vX.Y.Z`, merge `develop` into `main`.
3. Tag `main`: `git tag -a vX.Y.Z -m "vX.Y.Z"`, push `main` and the tag.
4. The `Release` workflow checks the tag against `plugin.json`, zips each skill folder (with `LICENSE`), and creates the GitHub release with the CHANGELOG section as notes. Tags with a `-` (betas) are marked as pre-releases.

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
