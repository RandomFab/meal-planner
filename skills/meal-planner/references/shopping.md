# Shopping list

Contents: 1. Which week · 2. Last week's leftovers · 3. Dishes without ingredients · 4. Needs · 5. Packs to buy · 6. What is already at home · 7. Staples and weekly extras · 8. Showing the list · 9. Writing to Notion · 10. Adding an item · 11. Never

Only if the profile's Shopping list module is on. Otherwise say so and offer to turn it on.

## 1. Which week

The list is for the next menu week that has Menu lines (usually the one just planned). It covers every Menu line of that week with Status Planned and a Dish, **except use-up days** (profile "Week"): those meals use what is left at home.

Lines with Status Leftovers or Lunchbox have no dish and count for nothing: their portions are already in the Servings of the meal they come from.

## 2. Last week's leftovers

Read the Shopping list lines of the previous week with Bought = no. If there are any, ask once, in the validation message (section 8): bought after all (tick Bought), carry over to this week (change Week), or drop (leave them, they stay unticked).

## 3. Dishes without ingredients

Planned dishes with Ingredients filled = no cannot be counted. List them under the shopping list: "I couldn't count: Chili, Quiche. Send me their ingredients (dictation or photo) and I'll add them." Build the list for the rest anyway. When the user sends the ingredients, complete the dish (`recipe.md` section 6), then add what it needs.

## 4. Needs

For each product:

```
need = Σ (Quantity of the Dish ingredients line × Servings of the Menu line)
```

summed over every counted Menu line. Read Quantity from Dish ingredients and Servings from Menu (rollups are not readable; see `notion-schema.md`).

Only products from recipes, staples and weekly extras go on the list. Never add a side, a drink or "something extra" yourself. If a meal looks incomplete, ask.

## 5. Packs to buy

- `packs = round up (need ÷ Recipe units per pack)`, written with the Pack size: "2 × 20 cl carton".
- Products bought loose (Recipe unit = piece, no Recipe units per pack): the number of pieces, rounded up: "3 carrots".
- Recipe units per pack empty for another unit: write the need in the recipe unit, rounded up ("4 tbsp"), and ask once whether to fill in the pack size.
- Free rules about buying (brand, label, organic) go in the Quantity text: "12 (free range)".

## 6. What is already at home

**Stock module on** (Level of each product):

| Level | Covers |
| --- | --- |
| Full | the week's need for a staple; any need smaller than one pack |
| Opened | about half a pack |
| Low, Out, empty | nothing |

Subtract what is covered. In doubt about an important product, ask in the validation message.

**Stock module off:** staples are assumed at home and not listed (section 7). Subtract only what the user said they have in this conversation ("we still have rice").

## 7. Staples and weekly extras

- **Staples** (Products with Staple = yes, and profile "Shopping"):
  - stock on: add the staples whose Level is Low or Out, Reason Staple;
  - stock off: ask in the validation message, "Running low on any staple?", and add what the user names.
- **Weekly extras** (profile "Shopping"): add each one, Reason Weekly extra. If the menu also needs the product, write one line with the larger of the two amounts ("12 eggs in total"). A category ("seasonal fruit: 3") becomes in-season products from Products; say which ones.
- **Never on the list** (profile "Shopping"): never add these, even if a recipe uses them; mention them in one line if a dish needs one.
- Missing product (weekly extra, or anything else to add): prepare it like `recipe.md` section 3, step 5, and show it with the list.

## 8. Showing the list

Grouped by store, then aisle in the order Fruit & veg, Meat & fish, Dairy, Savoury pantry, Sweet pantry, Frozen, Household. One line per product with the quantity. Store = the product's Store; if it is empty, follow the profile section "Stores" and propose to set it.

```
🛒 Supermarket
Fruit & veg: 3 carrots · 1 bunch of parsley
Dairy: 1 × 20 cl carton of cream · 12 eggs (free range)

🥕 Greengrocer
Fruit & veg: 4 apples
```

Then at most three lines: dishes not counted (section 3), questions (last week's lines, staples, doubts). No prices, no budget.

Wait for the user's yes. Apply corrections and show only what changed.

## 9. Writing to Notion

1. Read the Shopping list lines already on this Week. A product already listed: update its line rather than create a second one.
2. Create the new lines in one call: Item (product name), Product (always set), Quantity, Store, Aisle, Reason (Menu, Staple, Weekly extra, Added), Week = first day of the menu week, Bought = no.
3. Confirm in one line, and say which Notion view to open in the store (one per store).

## 10. Adding an item

"Add milk to the list": the request is the yes.

1. Find the product in Products. If it does not exist, create it (`recipe.md` section 3, step 5) and say so.
2. If it is already on the list for that week, update the quantity instead.
3. Create the line with Reason Added, Week = the next menu week not yet shopped for.
4. Confirm in one line ("Milk added to Supermarket, Dairy").

## 11. Never

- Never order, pay, or connect to a store.
- Never estimate prices or a budget.
- Never add a product that is not in a recipe, the staples, the weekly extras, or the user's request.
- Never add anything from "Never on the list" or containing a strict restriction.
- Never delete a Shopping list line.
