# Notion schema

Template version: 1.0

Contents: 1. Finding the workspace · 2. Household profile page · 3. Databases · 4. Reading · 5. Writing

## 1. Finding the workspace

The user's workspace is a copy of the Meal Planner template: a root page "Meal Planner" containing two pages (Start here, Household profile) and five databases (Menu, Shopping list, Dishes, Products, Dish ingredients).

1. If the Notion tools are not available, tell the user to connect Notion (Settings → Connectors → Notion) and to give it access to their Meal Planner page. Stop.
2. Search Notion for the page "Household profile". Open it and read the block "For Claude, do not edit" at the bottom.
3. If that block holds the five database addresses, use them. Fetch one; if it fails, go to step 4.
4. Otherwise, search for "Meal Planner" and open the root page. It lists the five databases. Note the data source address (`collection://…`) of each one.
   - Nothing found: tell the user to duplicate the template (link in Start here and in the README) and share it with Claude. Stop.
   - Several copies found: use the one whose Setup date is set; if none or several are, ask which one to use.
5. Check each database has the properties listed in section 3. If one is missing, tell the user which and stop: never work on a broken template.
6. Propose to write the addresses into the "For Claude, do not edit" block (setup does this). Until then, keep them for the conversation.

## 2. Household profile page

One section per heading. Each section starts with an italic sentence, then lines `Setting: value`. "(default)" after a value means the user has not set it yet; use the value anyway.

| Section | What it holds |
| --- | --- |
| Household | Members and appetite: adult 1, light 0.8, child 0.5 |
| Week | Planning day, first day of the menu, shopping day, use-up days |
| Meals | Meals planned per day, lunch at home / lunchbox / out per day, lunchbox rule |
| Stores | Store names and what is bought where |
| Never | Strict restrictions |
| Dislikes | Ingredients or dishes to avoid, with exceptions |
| Likes | Cuisines, favourite produce, comfort dishes |
| Protein habits | How often meat or fish, how much |
| Time | Maximum time: weekday lunch, weekday dinner, weekend |
| Equipment | Appliances |
| Variety | Repeat limits, new dishes per week |
| Rituals | Fixed meals |
| Shopping | Staples, weekly extras, never on the list |
| Recipes | Status given to a recipe the user sends |
| Modules | Shopping list, stock tracking, daily brief (on/off), brief time |
| Free rules | Anything else, in plain sentences |
| Journal | Dated lines: what Claude has learned |
| For Claude, do not edit | Template version, setup date, database addresses |

Editing: change only the line concerned, keep the italic sentence, remove "(default)" when the user sets a value. Journal: append one line at the end, `YYYY-MM-DD: <what was learned>`.

## 3. Databases

Exact names. Option lists are complete: never write another value.

### Menu — one line per meal

| Property | Type | Values |
| --- | --- | --- |
| Name | title | "<short day> <date> – <meal>" in the user's language, e.g. "Tue 12 – Dinner" |
| Date | date | the day |
| Meal | select | Lunch, Dinner |
| Dish | relation → Dishes | empty for a Lunchbox or Leftovers line without a dish |
| Status | select | Planned, Cooked, Leftovers, Lunchbox, Postponed, Skipped |
| Servings | number | portions to cook, lunchbox included |
| Extra for lunchbox | checkbox | cook extra portions tonight for tomorrow's lunchbox |
| Prep ahead | text | action and moment, e.g. "Take the salmon out of the freezer tonight" |
| Feedback | select | 👍, 😐, 👎 |
| Note | text | what the user said; origin of leftovers |

### Dishes — one page per dish, steps in the page body

| Property | Type | Values |
| --- | --- | --- |
| Name | title | short, user's language, no emoji |
| Status | select | Favorite, Approved, To try, Banned |
| Type | select | Everyday, Special, Weekend |
| Meal | multi-select | Lunch, Dinner |
| Total time (min) | number | |
| Season | multi-select | All year, Spring, Summer, Autumn, Winter |
| Main protein | select | Chicken, Pork, Beef, Duck, Fish, Eggs, Legumes, Tofu & soy, Veggie |
| Tags | multi-select | Good for leftovers, Oven, Freezes well, No cooking, Veggie option |
| Rating | select | ⭐ to ⭐⭐⭐⭐⭐ |
| Added from | select | Household, Suggested by Claude, Photo or link |
| Source | url | |
| Ingredients filled | checkbox | true once its Dish ingredients lines exist |
| Dish ingredients | relation → Dish ingredients | filled by creating the lines |
| Menu | relation → Menu | filled by Menu lines |
| Last cooked, Times cooked, Ingredients | rollups | Notion only, never write |

### Dish ingredients — one line per ingredient, for one adult portion

| Property | Type | Values |
| --- | --- | --- |
| Line | title | "<Dish> – <Product>" |
| Dish | relation → Dishes | |
| Product | relation → Products | |
| Quantity | number | in the product's Recipe unit, for one adult portion (0.125 = ⅛) |
| Note | text | only what the recipe says ("yolk only") |
| Product name, Unit, Label | rollups, formula | Notion only, never write |

### Products — one line per product: catalogue, and stock if the module is on

| Property | Type | Values |
| --- | --- | --- |
| Name | title | singular, unless sold in plural ("Peas") |
| Store | select | the user's stores (options created at setup) |
| Aisle | select | Fruit & veg, Meat & fish, Dairy, Savoury pantry, Sweet pantry, Frozen, Household |
| Recipe unit | select | piece, pack, can, tbsp, tsp, knob, slice, clove, handful, bunch, tray, sachet, g, ml |
| Pack size | text | what is bought: "20 cl carton", "500 g pack" |
| Recipe units per pack | number | e.g. 13 tbsp in a 20 cl carton of cream |
| Season | multi-select | as Dishes |
| Staple | checkbox | always kept at home |
| Location | select | Fridge, Freezer, Pantry |
| Level | select | Full, Opened, Low, Out; empty = not tracked |
| Note | text | |
| Used in, Shopping list | relations | filled by the other databases |

### Shopping list — one line per product to buy

| Property | Type | Values |
| --- | --- | --- |
| Item | title | product name |
| Product | relation → Products | always set |
| Quantity | text | in packs: "2 × 20 cl carton", "3 carrots" |
| Store | select | same options as Products |
| Aisle | select | same options as Products |
| Reason | select | Menu, Staple, Weekly extra, Added |
| Week | date | first day of the menu week |
| Bought | checkbox | |

## 4. Reading

- Query databases with SQL on the data source when the connector allows it; otherwise fetch the views.
- **Rollups and formulas are not readable through the API** (Last cooked, Times cooked, Ingredients, Product name, Unit, Label). Compute instead:
  - ingredients of a dish: Dish ingredients where Dish contains the dish, joined to Products (Name, Recipe unit);
  - last time a dish was eaten: latest Menu Date where Dish contains it and Status is Cooked or Leftovers.
- Relations are stored as JSON arrays of page URLs.

## 5. Writing

- Dates: `date:<Property>:start` = `YYYY-MM-DD`, `date:<Property>:is_datetime` = 0.
- Relations: array of page URLs or IDs.
- Checkboxes: `__YES__` / `__NO__`.
- Create several pages of one database in a single call. When later steps need the new pages' URLs (Products, then Dishes, then Dish ingredients), wait for the call to return them.
- Before creating a line, check it does not already exist (same dish name, same product name, same date and meal). Update it instead of duplicating.
- Never delete a page. Unlink or change the status instead.
