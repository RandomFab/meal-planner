# Recipes: adding and fixing dishes

Contents: 1. Which path · 2. Quick list · 3. Full recipe · 4. Dish properties · 5. Page body · 6. Completing a dish later · 7. Fixing a dish · 8. Never

## 1. Which path

| The user sends… | Path |
| --- | --- |
| Dish names only ("we often make carbonara, chili, quiche") | Quick list (section 2) |
| A photo, a scan, a screenshot, a link, a dictated or typed recipe | Full recipe (section 3) |
| Ingredients for a dish that already exists without them | Completing a dish later (section 6) |

Several recipes at once: handle them one by one (show, approve, create), unless the user asks to approve them all together.

## 2. Quick list

1. Split the message into dish names. Check each one against Dishes (same or very close name): an existing dish is not created twice, say so.
2. Check each name against the profile section "Never". A dish that obviously contains a strict restriction is not added: say why.
3. Show the list of dishes to create, with only what you are sure of: Name, Status (from the profile section "Recipes"), Added from = Household, Ingredients filled = no. If you add estimates (Type, Meal, Total time, Season, Main protein), show them in one line per dish, marked as estimates, so the user can correct them in one reply.
4. After a yes, create the dishes in one call.
5. Confirm in one line: how many dishes were added, and that their ingredients will be asked for when a shopping list needs them. Offer to plan a week now.

## 3. Full recipe

1. **Read the source.** If part of it is unreadable or missing (quantity, step, time), say what is missing and ask. Never fill the gap yourself.
2. **Look for duplicates.** Search Dishes for the same or a close dish (name or main ingredient). If found, ask: update that dish, or create a new one?
3. **Check restrictions.**
   - Profile "Never": flag every ingredient concerned **before** showing anything else, and propose an adaptation (substitute or removal). Never save the original version.
   - Profile "Dislikes": point it out and propose an adaptation; the user decides.
4. **Bring it to one adult portion.** Divide every quantity by the number of servings the recipe makes. If the recipe does not say how many servings, ask.
5. **Match every ingredient to a product.**
   - Search Products for the existing product (singular name: "Egg", "Tomato"). Always reuse it, never create a near-duplicate ("cream" is the product Cream).
   - Write the quantity in the product's Recipe unit, as a decimal: ⅛ = 0.125, ⅙ = 0.167, ¼ = 0.25, ⅓ = 0.333, ½ = 0.5, ⅔ = 0.667, ¾ = 0.75.
   - Prefer simple kitchen units (pieces, spoons, fractions of a pack) over grams. Use g or ml only if the recipe or the user works that way.
   - Missing product: prepare it with Name, Store, Aisle, Recipe unit, Pack size, Recipe units per pack, Season, Location, and Staple if it is in the profile's staples. Store: the only store if there is one; otherwise follow the profile section "Stores", or ask. If you do not know the usual pack size, write the most common one and say it is an estimate.
   - Salt, pepper, water and common dried spices or herbs: no product. Write them in the page body as one line, "*Seasoning: …*".
6. **Show the dish** in the chat: properties, readable ingredient list ("⅛ pack of bacon"), new products to create, steps, and the questions left. If the dish calls for a side the recipe does not include, ask in one sentence ("Rice or green beans would go well with it, shall I add them?"). Never add it yourself.
7. **Wait for the user's yes.** Apply corrections and show only what changed.
8. **Create, in this order**, waiting for each call to return the new URLs:
   1. the missing products;
   2. the dish (Ingredients filled = yes), with its page body;
   3. all its Dish ingredients lines, in one call.
9. **Confirm** in one line with the link to the dish. Mention new products and anything still to confirm.

## 4. Dish properties

| Property | Rule |
| --- | --- |
| Name | Short, in the user's language, no emoji |
| Status | From the profile section "Recipes" for a recipe the user sends (default Approved). To try for a dish Claude suggests, or if the user says they have not made it yet |
| Type | Everyday: simple, could come back every week. Special: more elaborate. Weekend: needs more time than a weekday allows |
| Meal | Lunch if total time ≤ the profile's weekday lunch time; Dinner if ≤ weekday dinner time; both if it fits both |
| Total time (min) | Preparation plus cooking. If the source does not say, estimate and say so |
| Season | From the main fresh ingredients; All year if none is seasonal |
| Main protein | The main source of protein; Veggie if none of the others |
| Tags | Good for leftovers (keeps and reheats well), Oven, Freezes well, No cooking, Veggie option (meat or fish can simply be left out) |
| Added from | Household (typed, dictated or listed), Photo or link, Suggested by Claude |
| Source | The URL, for a link |
| Rating | Only if the user gives one |

## 5. Page body

```markdown
*Seasoning: salt, pepper, nutmeg.*

1. Preheat the oven to 180 °C.
2. …

*Prep ahead: make the pastry the day before and keep it in the fridge.*
```

- Short steps, one action each, with times and temperatures.
- A "*Prep ahead: …*" line for anything to do in advance (thawing, soaking, marinating, dough, resting). The weekly plan and the daily brief use it.
- If the profile lists an appliance that clearly helps (for example a food processor for pastry), add a short "*Tip: …*" line.
- Quantities estimated by you: add "*Quantities to adjust after the first try.*".

## 6. Completing a dish later

A dish with Ingredients filled = no came from a quick list. When the user gives its ingredients (or the shopping list asks for them):

1. Follow section 3 from step 3, for the ingredients and steps only.
2. After the yes, create the products and Dish ingredients lines, add the steps to the page body, set Ingredients filled = yes.

## 7. Fixing a dish

Only when the user asks, or accepts your proposal:

- Change a quantity: update the Quantity of the Dish ingredients line.
- Add an ingredient: create a Dish ingredients line.
- Remove an ingredient: empty the Dish relation of its line. Do not delete the page.
- Change the steps: edit only the part of the page body concerned.
- Change a property: update it, using only the values listed in the schema.

## 8. Never

- Never save a dish containing a strict restriction.
- Never create a dish or a product that already exists.
- Never invent ingredients, quantities, steps or times missing from an unreadable source.
- Never add sides, optional ingredients or alternatives the recipe does not have, unless the user agrees.
- Never change or delete an existing dish or product without the user's request.
- Never write calories or nutrition figures.
