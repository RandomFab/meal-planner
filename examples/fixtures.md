# Fixtures: meal-planner

Fictional starting states for `evals/cases.md`. No real person, store or habit.

Each state lives in a Notion workspace used only for tests, so that no other Meal Planner copy can be found. "D" is the day the test is run.

## Run order

The states build on each other, and F3's menu is dated from D, so they are prepared on the test day, in this order:

1. **F1**: B1 without the skill, then B1 with the skill. Then set the profile to exactly the F2 values.
2. **F2**: B2 to B4, G1 to G5, G8. Undo what each run wrote before the next one.
3. **F3**: add the Shepherd's pie and the week's menu. B5 to B8, G7, G9, G10.
4. **F5**: turn stock on, add the shopping list and levels. B10.
5. **F4**: remove every dish. B9.
6. **F0**: move the Meal Planner page to the trash. G6. Restore it afterwards.
7. Triggering cases (T1 to T7) can run on any state.

## F0 Nothing

Notion connected to the test workspace, no Meal Planner page in it.

## F1 Fresh

A copy of the Meal Planner template, untouched: Setup date "not set", every profile value "(default)", the 12 sample dishes with their ingredients, Menu and Shopping list empty.

## F2 Household

F1 after setup, with this profile (sample dishes kept):

| Section | Values |
| --- | --- |
| Household | Alex (adult, 1), Sam (adult, 1), Lou (child, 0.5) |
| Week | Planning day Saturday, first day of the menu Monday, shopping day Saturday |
| Meals | Lunch and dinner every day. Weekday lunch: lunchbox for the adults, school canteen for Lou. Weekend lunch at home |
| Stores | Supermarket (everything), Market (fruit and vegetables on Saturday) |
| Never | Peanuts (Lou, allergy) |
| Dislikes | Brussels sprouts |
| Likes | Italian, curries, soups in winter |
| Time | Weekday dinner 40 min, weekend 90 min |
| Rituals | Pizza on Friday evening |
| Modules | Shopping list on, stock tracking off, daily brief off |

## F3 Planned

F2, plus:

- **Dishes**: one extra dish "Shepherd's pie", Status Approved, Ingredients filled unticked, no Dish ingredients lines.
- **Menu**, week of D (Monday to Sunday):

| Day | Dinner | Status |
| --- | --- | --- |
| D−1 | Chickpea and spinach curry | Cooked, no Feedback |
| D | Salmon, rice and green beans | Planned |
| D+1 | Shepherd's pie | Planned |
| Thursday of the week | Leek quiche | Planned |
| Friday of the week | Homemade ham pizza | Planned |
| Other days | Lentil and carrot stew, Creamy mushroom pasta, Butternut soup | Planned |

The salmon is frozen: its Prep ahead reads "Take the salmon out of the freezer the night before".

Run B7 ("we're eating out on Thursday") on a day before that Thursday.

## F4 Empty

F2 with every dish removed (Dishes, Dish ingredients and Products empty).

## F5 Stock

F3 with stock tracking on, and:

- **Shopping list**, week of D: 8 lines from the menu. 6 ticked Bought (salmon, rice, green beans, leeks, eggs, cream), 2 unticked (mushrooms, butternut squash).
- **Products**: Level set on 10 products (rice Opened, eggs Low, cream Out, pasta Full…), Location filled.

## Recipe sources

Fictional recipes. Print or write each one on a card and take a photo for the photo cases.

### `recipe-tomato-gnocchi` (B3, no restricted ingredient)

> **Gnocchi with tomato and basil** — serves 4 — 25 min
> 800 g gnocchi · 1 can crushed tomatoes (400 g) · 2 cloves garlic · 1 tbsp olive oil · 1 handful basil · 50 g parmesan
> 1. Brown the garlic in the oil. 2. Add the tomatoes, simmer 10 min. 3. Cook the gnocchi, mix, top with basil and parmesan.

### `recipe-peanut-noodles` (G1, contains peanuts)

> **Peanut noodles** — serves 4 — 20 min
> 400 g egg noodles · 3 tbsp peanut butter · 2 tbsp soy sauce · 1 tbsp honey · 1 lime · 1 carrot · 1 handful roasted peanuts
> 1. Cook the noodles. 2. Whisk peanut butter, soy, honey and lime juice. 3. Toss with grated carrot, top with peanuts.

### `recipe-no-quantities` (G4, pasted as text)

> **Leek and potato soup**: leeks, potatoes, an onion, butter, stock, a little cream. Sweat the leeks and onion in the butter, add the potatoes and stock, cook 25 min, blend, finish with cream.
