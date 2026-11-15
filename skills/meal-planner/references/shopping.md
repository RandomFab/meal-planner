# Shopping list

Contents: 1. How the list works · 2. Dishes without ingredients · 3. Showing the list · 4. Adding an item · 5. Weekly extras and staples · 6. At the store · 7. Never

Only if the profile's Shopping list module is on. Otherwise say so and offer to turn it on.

## 1. How the list works

Notion computes the list. Claude never writes it line by line: there is no shopping list database, only a view of Products on the **Shopping list** page.

For each product that is not a Staple:

```
need    = Σ Quantity (Dish ingredients) × Servings (Menu)
          over Menu lines with Status Planned, from today to today + 6
stock   = see stock.md section 1
to buy  = need − stock, rounded up to whole packs
```

- Staples (Staple = yes) are never computed: they are on the list only when Add to list is ticked.
- Add to list ticked, nothing else needed: one pack.
- The view "To buy" shows every product with something to buy, grouped by Store, sorted by Aisle, with the dishes it is for (For dishes) and a **Bought** button.
- A product leaves the list as soon as: Bought is pressed (Bought since grows by what was bought, Add to list is unticked), the menu changes, or a count shows there is enough at home.

So, to change the list, change what it is computed from: the menu (`feedback.md`), the quantities of a dish (`recipe.md` section 7), the stock (`stock.md`), or Add to list. Never write the formula properties (`notion-schema.md`).

The list covers 7 days from today. Meals further ahead appear as the days come. If the user asks for a longer stretch, say so; the window is the `6` in the Need 7d formula, which they can change in Notion.

## 2. Dishes without ingredients

A planned dish with no Dish ingredients lines adds nothing to the list. Each time you show the list, read the Menu lines of the next 7 days (view "Next 7 days"), and list the dishes with Ingredients filled = no under the list: "Not counted: Chili, Quiche. Send me their ingredients (dictation or photo) and I'll add them." When the user sends them, complete the dish (`recipe.md` section 6). The list updates by itself.

## 3. Showing the list

"Make the shopping list", "what do we need?":

1. Read the "To buy" view (view mode, address in the profile block "For Claude, do not edit"). You get the products, their Store and Aisle. The quantities are formulas, not readable.
2. Show the products grouped by store, then aisle in the order Fruit & veg, Meat & fish, Dairy, Savoury pantry, Sweet pantry, Frozen, Household. Say that the quantities and the Bought buttons are on the Shopping list page.

```
🛒 Supermarket
Dairy: cream · mozzarella · buckwheat galettes
Meat & fish: cod · ham

🥕 Greengrocer
Fruit & veg: leeks · mushrooms · parsley · potatoes

Quantities and ✓ buttons: Shopping list page in Notion.
```

3. Then at most three lines: dishes not counted (section 2), "Running low on any staple?", a product from "Never on the list" that a dish needs.

No prices, no budget.

## 4. Adding an item

"Add milk to the list", "we're out of oil": the request is the yes.

1. Find the product in Products. If it does not exist, create it (`recipe.md` section 3, step 5) and say so.
2. Tick Add to list. It adds one pack; if the user wants more, say it is noted as one pack and they can buy what they need.
3. Confirm in one line: "Milk is on the list (Supermarket, Dairy)."

## 5. Weekly extras and staples

- **Weekly extras** (profile "Shopping"): after a week is saved, tick Add to list on each one. The Bought button unticks them; next week, tick them again. A category ("seasonal fruit") becomes in-season products from Products; say which ones.
- **Staples** (profile "Shopping", Staple = yes): not counted. When the user says one is running low, tick Add to list.
- **Never on the list** (profile "Shopping"): these products have Staple = yes and are never ticked, so they never appear. Mention them in one line if a planned dish needs one.

## 6. At the store

The user presses Bought on each line as they go. Nothing to do for Claude.

- "I didn't find the leeks": nothing to write, they stay on the list. If a meal of today or tomorrow needs them, propose a change (`feedback.md` section 3).
- "I bought two instead of one", "I also bought feta", "I pressed Bought by mistake": ask how many there are at home now if it is not clear, then count it (`stock.md` section 2).

## 7. Never

- Never order, pay, or connect to a store.
- Never estimate prices or a budget.
- Never tick Add to list on a product the user did not ask for, that is not a staple running low and not a weekly extra.
- Never tick a product from "Never on the list" or containing a strict restriction.
- Never write the formula properties (Need 7d, Eaten since, Stock, Buy qty, To buy, For dishes).
