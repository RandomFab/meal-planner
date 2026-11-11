# Setup, settings and modules

Contents: 1. When · 2. Before the questions · 3. The three messages · 4. Summary and writing · 5. Sample dishes · 6. First dishes · 7. First menu · 8. To finish · 9. Changing a setting · 10. Modules · 11. Never

## 1. When

- The user says "set up my meal planner", or the same in their language.
- The profile's "Setup date" is "not set" and the user asks for something: answer a quick request with the defaults, then offer setup.
- The user wants to change a setting or turn a module on or off: sections 9 and 10 only.

Tone: welcoming, short. The whole setup should take about 10 minutes.

## 2. Before the questions

1. **Access and template**: follow "Finding the workspace" in `notion-schema.md`. If it fails, explain and stop.
2. **Template version**: read it in the "For Claude, do not edit" block. If it is not the version in `notion-schema.md`, say which properties differ and stop.
3. **Profile already filled** (Setup date set, or values without "(default)"): do not start over. Show the profile in a few lines and ask which sections to review.
4. **Open with one sentence**: "Three short questions to get to know your household, then I'll propose your first week. Skip anything: I'll use the default."

## 3. The three messages

One message each, 3 or 4 questions at most, each with its default in brackets. "I don't know", "skip" or no answer keeps the default. Accept answers in any form, all at once or bit by bit.

**Message 1, household and week**

- Who eats at home? Number of adults and children, and whether someone eats less or more (appetite: adult 1, light 0.8, child 0.5). [2 adults]
- Which day do you plan the menu, which day does it start, and when do you shop? [plan Saturday, start Monday, shop Saturday]
- Where do you shop, and what do you buy where? [one supermarket for everything]
- Lunch: at home, packed lunch or out, and on which days? [at home every day]

**Message 2, what you don't eat**

- Anything nobody can eat: allergy, intolerance, diet, religion? [none]
- Ingredients or dishes you dislike, with exceptions ("no cabbage, broccoli is fine")? [none]
- Meat and fish: how often, and how much? [no rule]

If a strict restriction is given, add the medical disclaimer once: you help, but you are not a medical tool, and labels must always be checked.

**Message 3, what you like**

- Favourite cuisines, vegetables, comfort dishes? [not set]
- Maximum cooking time: weekday lunch, weekday dinner, weekend? [20 / 45 / 90 min]
- Kitchen appliances beyond oven and hob (food processor, rice cooker, slow cooker)? [oven, hob]
- Any fixed meal ("Friday: pizza")? [none]

Everything else keeps its default (Variety, Shopping, Recipes, Modules). Mention it in the summary: the user can change it now or later.

## 4. Summary and writing

1. **Show the summary**: one line per section, in the user's language, defaults marked. End with the disclaimer if there is a strict restriction, and "Shall I save it?"
2. **After the yes**, in this order:
   1. **Profile page**: for each section, replace the values the user gave and remove "(default)". Keep headings, setting names and italic sentences exactly, in English. **Write the values in the user's language, never translated into English**: a French speaker gets "Cacahuètes", "Cuisine italienne", "Vendredi soir : pizza", not "Peanuts", "Italian cuisine".
   2. **Stores**: add each store as an option of Store, with the same name in Products and Shopping list. Create one Shopping list view per store, built like the "Supermarket" view (list, filter Store = the store and Bought unticked, grouped by Aisle). If the user does not shop at a "Supermarket", rename that view and change its filter to their main store.
   3. **Products' Store**: set every product to the right store, following the profile section "Stores" (one store: all products).
   4. **Staples**: tick Staple on the products the profile lists as staples.
   5. **"For Claude, do not edit" block**: Setup date (today) and the five data source addresses.
3. **Confirm** in one line: "Your profile is saved. You can change anything by telling me, or directly on the Household profile page." Then, in the same message, go on to section 5.

Setup is the only time you may create select options (Store only).

**After saving, sections 5 to 8 always run, in this order, one short message each.** Skip none, even when the user has already answered part of them: each message ends with its own question.

## 5. Sample dishes

The template comes with 12 sample dishes, Status To try, Added from Suggested by Claude:

Tomato and mozzarella pasta salad · Lentil and carrot stew · Homemade ham pizza · Roast chicken thighs and vegetables · Chickpea and spinach curry · Leek quiche · Salmon, rice and green beans · Mushroom risotto · Butternut soup · Bean chili · Creamy mushroom pasta · Omelette and green salad

1. **Strict restrictions first**: every sample dish that contains something in "Never" gets Status Banned. Say which, or say that none does.
2. **Always ask**, never decide for the user: "Keep the other sample dishes to start, or remove them?" [keep]. If the user's language is not English, add in the same question: "Shall I translate their names and steps into <language>?" [yes]
3. **Remove**: move those dish pages and their Dish ingredients lines to the Notion trash. This is the only deletion allowed, only for these 12 dishes, only during setup, only after the yes. Products stay: they are useful for your own recipes.
4. **Translate**: if the user agreed, rename the kept dishes and rewrite their steps in the user's language. Product names follow too.

## 6. First dishes

Present the four ways in a few lines:

- ⚡ Quick list: "we often make carbonara, chili, quiche": added by name, ingredients asked for later
- 🎙️ Dictation: voice input on the phone, read the recipe aloud
- 📸 Photo: a cookbook page, a handwritten card, a screenshot
- 🔗 Link: the address of a recipe page

Then: "Shall we start with the quick list? Name 5 to 10 dishes you often make." [skip] Follow `recipe.md` section 2.

## 7. First menu

Its own message, or the last line of the previous one, never buried in a paragraph: "Shall I propose your first week, from <first day of the next menu, with its date>?" [yes] Follow `plan-week.md`. A short history is normal: say that the menus get better with feedback.

## 8. To finish

Once the first menu is saved or declined, show in the user's language:

- Five sentences to try: "What's for dinner?", "Make the shopping list", "We're eating out on Thursday", "The curry was great 👍", a photo of a recipe.
- Where things are: the Today view of Menu on the phone, one Shopping list view per store.
- Optional modules (section 10): stock tracking and the daily brief. Offer them in one line, do not push.

## 9. Changing a setting

"We're three now", "no more fish", "lunch at the office on Tuesdays":

1. Find the section and line concerned. Show the line before and after.
2. After the yes, change only that line, remove "(default)", and add one Journal line.
3. A new store: also add the Store option and its view (section 4, step 2). A new staple: also tick Staple on the product.
4. A change that affects the planned week (a new strict restriction, fewer people): check the Menu lines from today on and propose the changes (`feedback.md` section 3).

## 10. Modules

Turn a module on or off only when the user asks or agrees. Update the line in the profile section "Modules".

| Module | On | Off |
| --- | --- | --- |
| Shopping list | `shopping.md` is used | No list; the menu still works |
| Stock tracking | Say that Claude will update the levels after shopping and cooking without asking each time. Offer the first check (`stock.md` section 2). Point to the "At home" view of Products | Levels stay as they are and are no longer read |
| Daily brief | See below | Tell the user to delete their scheduled task |

**Daily brief**: it needs a scheduled task in the user's Claude app (available on some plans only). Give the text to paste, with the time from the profile:

```
Every day at 10:00: give me my daily meal brief from my Meal Planner.
```

Without scheduled tasks, the user can simply ask "what's for dinner?" each day.

## 11. Never

- Never write the profile before the summary is approved.
- Never write profile values in English for a user who speaks another language.
- Never end the setup without asking about the sample dishes and offering the first week.
- Never ask more than 4 questions in one message.
- Never delete anything, except the sample dishes the user asked to remove during setup.
- Never change the headings, setting names or italic sentences of the profile page.
