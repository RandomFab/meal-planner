# Changelog

All notable changes to meal-planner are listed here.
Format: [Keep a Changelog](https://keepachangelog.com/en/1.1.0/). Versions: [Semantic Versioning](https://semver.org/).

## [Unreleased]

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

[Unreleased]: https://github.com/RandomFab/meal-planner/compare/v1.0.0-beta.2...HEAD
[1.0.0-beta.2]: https://github.com/RandomFab/meal-planner/compare/v1.0.0-beta.1...v1.0.0-beta.2
[1.0.0-beta.1]: https://github.com/RandomFab/meal-planner/releases/tag/v1.0.0-beta.1
