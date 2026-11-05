# Stock: what is left at home

Contents: 1. Levels · 2. First check · 3. Putting the shopping away · 4. After cooking · 5. Fridge check · 6. What can we make? · 7. Never

Only if the profile's Stock tracking module is on. Otherwise say so and offer to turn it on (`setup.md`).

Turning the module on authorises the level updates in sections 3 and 4: write them without asking, and list them in the confirmation line. Everything else is proposed first.

## 1. Levels

| Level | Means |
| --- | --- |
| Full | unopened, or plenty left |
| Opened | in use, about half left |
| Low | almost gone: a staple at Low goes on the next shopping list |
| Out | none left |
| empty | not tracked |

Levels are approximate on purpose. No quantities, no use-by dates.

## 2. First check

When the module has just been turned on, no product has a Level yet. Offer a first check in one message: "Tell me what's in your fridge, freezer and pantry, roughly. A photo works too."

- Match each item to an existing product; create the missing ones (`recipe.md` section 3, step 5).
- Set Level (Full unless the user says it is opened or almost gone) and Location (Fridge, Freezer, Pantry).
- Show the result grouped by Location, wait for the yes, then write in one call per database.

## 3. Putting the shopping away

When the user says the shopping is done, or the day after the profile's shopping day:

1. Read the Shopping list lines of that week.
2. Lines with Bought = yes: set the product's Level to Full, and Location if it is empty.
3. Lines with Bought = no: one grouped question ("Not found: cream, leeks?"). If a missing product is needed for a planned meal, propose a change (`feedback.md` section 3).
4. Confirm in one line: how many products are now Full, and what is missing.

If the user did not tick anything, ask: "Did you get everything on the list?" A yes ticks every line.

## 4. After cooking

When a Menu line becomes Cooked (`feedback.md`), for each Dish ingredients line of its dish:

```
used = Quantity × Servings, compared with Recipe units per pack
```

Lower the product's Level roughly:

- less than a quarter of a pack: no change;
- a quarter of a pack up to a whole pack: one step down (Full → Opened → Low → Out);
- a whole pack or more: Out, unless the user bought several.

Products with an empty Level stay empty. Name the changes in the confirmation ("Cream now Low"). A staple that reaches Low goes on the next shopping list (`shopping.md` section 7).

## 5. Fridge check

When the user talks about what is left, or asks for a check:

1. Read Products with a Level other than Out (view "At home"), grouped by Location, Opened and Low first.
2. Show it in a few lines and ask for corrections in one go: "Anything finished? Anything new?"
3. Update the Levels. What is gone: Out (never delete the product). Something new: the existing product, else create it.

## 6. What can we make?

"What can we make with what's left?":

1. Start from products Opened or Low, fresh ones first (Fridge before Pantry).
2. Find the dishes that use them (Dish ingredients), excluding Banned dishes and anything with a strict restriction.
3. Keep dishes in season, that fit today's time limit, and whose other ingredients are Full or Opened.
4. Propose 2 or 3, each with the products it uses up. If the user picks one, offer to put it on the menu (`feedback.md` section 3).

## 7. Never

- Never delete a product: set it to Out.
- Never track use-by dates or exact quantities.
- Never set a Level the user or the shopping list did not give, except the estimate after cooking.
