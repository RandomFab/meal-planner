# Stock: what is at home

Contents: 1. How stock works · 2. Counting · 3. Fridge check · 4. What can we make? · 5. Never

## 1. How stock works

Notion computes the stock of every product that is not a Staple:

```
Stock = Stock count + Bought since − Eaten since
```

- **Stock count** and **Counted on**: the last count, what was there before the meals of that day. Empty Counted on: the template's start date.
- **Bought since**: what the Bought button of the shopping list added since the count.
- **Eaten since**: Σ Quantity × Servings over the Menu lines dated from Counted on, with Status Cooked, or Status Planned and a date before today.

What follows from it:

- Nobody updates the stock after cooking. A planned meal that was not eaten at home must become Skipped or Postponed (`feedback.md`), otherwise its ingredients count as used.
- Staples are not counted (`shopping.md` section 5).
- The stock drifts: food eaten outside the menu, thrown away, estimated quantities. A count fixes it.

**Stock is a formula: you cannot read it.** When you need the stock of a few products, compute it with the same rule from what you can read: Stock count, Counted on, Bought since (Products), the Menu lines of their dishes, and the Quantity of their Dish ingredients lines. Never do it for the whole catalogue.

## 2. Counting

The user says what is there: "3 steaks left", "no more cream", "half a carton of cream", a photo of the fridge. The message is the request: write, then confirm in one line.

For each product:

1. Find it in Products; if it does not exist, create it (`recipe.md` section 3, step 5).
2. Write, in one call per product:
   - Stock count = the quantity in the product's Recipe unit ("half a carton" with 13 tbsp per carton = 6.5);
   - Counted on = today, or tomorrow if the count is made after a meal of today ("tonight there are 2 left");
   - Bought since = 0.
3. Vague amounts ("a bit of parmesan"): estimate, and say it is an estimate.
4. "None left", "finished": Stock count 0.
5. A Staple: no count. "No more oil" means Add to list (`shopping.md` section 4).

Confirm: "Counted: 3 steaks, cream 0 (on the list again if a dish needs it)."

## 3. Fridge check

When the user wants to check what is left, or the day after shopping if they ask for it:

1. Point to the "At home" view of Products: every counted product, grouped by place, the largest stocks first.
2. Ask for corrections in one go: "Anything wrong? Tell me what is really there, roughly."
3. Count what the user names (section 2).

## 4. What can we make?

"What can we make with what's left?":

1. Start from fresh products (Location Fridge) with a Stock count or Bought since above 0. Compute their stock (section 1); keep those above 0.
2. Find the dishes that use them (Dish ingredients), excluding Banned dishes and anything with a strict restriction.
3. Keep dishes in season, within today's time limit.
4. Propose 2 or 3, each with the products it uses up. If the user picks one, offer to put it on the menu (`feedback.md` section 3).

## 5. Never

- Never delete a product: count it 0.
- Never write the formula properties.
- Never set a count the user did not give, except an estimate of a vague amount, said as such.
- Never track use-by dates.
