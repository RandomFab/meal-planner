# Changelog

All notable changes to meal-planner are listed here.
Format: [Keep a Changelog](https://keepachangelog.com/en/1.1.0/). Versions: [Semantic Versioning](https://semver.org/).

## [Unreleased]

### Fixed

- The shopping list now covers today and the 7 days after it, so a list made the day before your menu week starts no longer misses the week's last day. Template 2.0 users: paste the new Need 7d and For dishes formulas from `docs/developers.md`.
- When a product you expected is not on the list, Claude now tells you why (meal too far ahead, enough at home according to the last count…) instead of saying it can't check.
- When Claude changes a product (frozen to fresh, another pack size), it asks how many are at home instead of keeping the old count.
- The morning brief arrives once, with no recap and no talk of skills, tools or notifications. The scheduled task runs without the skill, so Claude now writes it with all the rules it needs. Already have one? Write "Fix my morning brief task" and paste the new instructions into it.

## [1.0.0-beta.3] - 2026-11-15

### Changed

- The install video in the README is now a sharper video, played right in the page.
- Claude Code: install with `/plugin install meal-planner@randomfab`, from the new `RandomFab/claude-plugins` catalogue.

## [1.0.0-beta.2] - 2026-11-15

### Added

- A short video of the whole install, in the README.

### Changed

- The shopping list is now computed by Notion and always up to date: change a dish in the menu and the list follows. It covers the next 7 days and says which dish each product is for.
- What is at home is counted, not guessed: it goes up when you press Bought in the store and down when a meal is eaten. Tell Claude "3 steaks left" to correct it.
- Basics you don't count (oil, spices, butter…) go on the list only when you say they are running low.
- Template 2.0: the Shopping list database is replaced by a Shopping list page; Products gets the stock and shopping properties. Duplicate the new template.

### Removed

- The stock tracking module: stock is now part of the shopping list.

## [1.0.0-beta.1] - 2026-11-11

First beta, for the first testers.

### Added

- Guided setup: a few short questions about your household, a summary to approve, then your first week of meals.
- Four ways to add a recipe: a list of dish names, dictation, a photo, or a link.
- Weekly menu built from your dishes, your tastes and your rules, saved to Notion once you agree.
- Shopping list sorted by shop and aisle, with quantities worked out from your recipes.
- Daily meal brief: today's dishes and what to prepare for tomorrow, on request or every morning.
- Feedback and changes of plan: say what you ate, what you thought of it, or that you're eating out, and the week adapts.
- Optional tracking of what is left in the fridge, freezer and cupboards.

[Unreleased]: https://github.com/RandomFab/meal-planner/compare/v1.0.0-beta.3...HEAD
[1.0.0-beta.3]: https://github.com/RandomFab/meal-planner/compare/v1.0.0-beta.2...v1.0.0-beta.3
[1.0.0-beta.2]: https://github.com/RandomFab/meal-planner/compare/v1.0.0-beta.1...v1.0.0-beta.2
[1.0.0-beta.1]: https://github.com/RandomFab/meal-planner/releases/tag/v1.0.0-beta.1
