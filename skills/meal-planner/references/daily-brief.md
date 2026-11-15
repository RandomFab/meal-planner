# Daily brief

Contents: 1. When · 2. Read · 3. Message · 4. Rules · 5. Scheduled run · 6. Never

The brief only reads. It informs and proposes; it never writes to Notion.

## 1. When

- The user asks "what's for dinner?", "what do we eat today?".
- A scheduled task runs it, if the profile's Daily brief module is on (time in the profile).

## 2. Read

1. **Today's date**, from the context or a tool, in the user's time zone. Never guess it.
2. **Menu**: lines for yesterday, today and tomorrow.
3. **Dishes of today**: Total time, and the Prep ahead line of the page body (in the user's language, `recipe.md` section 5).
4. **Menu lines of today and tomorrow**: Prep ahead, Servings, Extra for lunchbox, Status.
5. **Yesterday**: lines still Planned, or Cooked without Feedback.
6. **Missing products**, only if the shopping list module is on: the products of today's and tomorrow's dishes (Dish ingredients) that are still in the "To buy" view.
7. **Profile "Week"**: is today the shopping day, a use-up day, or the day after shopping?

## 3. Message

Short, readable on a phone, in the user's language:

```
🍽️ Today, Tuesday 13 Oct.
• Lunch: Pasta with pesto (15 min)
• Dinner: Leek quiche (55 min), 2 people + 1 lunchbox 🥡

⏰ Prep ahead
• Today: make the pastry before 7 pm
• For tomorrow: take the salmon out of the freezer tonight

💬 Last night, the chili: 👍 😐 👎?
```

Add, only when they apply:

- **Lunchbox**: "Lunch: lunchbox (leftovers of …)" on a Lunchbox line; "+ 1 lunchbox 🥡" on a dinner with Extra for lunchbox.
- **Leftovers**: "Lunch: leftovers of …".
- **Use-up day**: "Use-up day: finish what's left."
- **Shopping day** (shopping module on): "Shopping day: your list is ready in Notion."
- **Day after shopping** (shopping module on): "Bought something different from the list? Tell me and I'll fix the stock."
- **Missing ingredient** (shopping module on): a product of today's or tomorrow's dish still to buy: "The cream for tonight's quiche is still on the list. Swap with Thursday?"

## 4. Rules

- The Prep ahead section is always there, for **today and tomorrow**. If there is nothing: "Nothing to prepare."
- Feedback reminder: only yesterday's meals, one line. If the three days before also have no feedback at all, skip it: the user is not giving feedback right now.
- **No menu today**: say so, and propose 2 quick dishes (Favorite or Approved, within today's time limit, in season, from what is at home). If the coming days are empty too, offer to plan the week.
- When the user replies (feedback, change of plan), follow `feedback.md`.

## 5. Scheduled run

- Send the message with the tool that notifies the user, so it reaches their phone.
- Nobody is there to answer: ask nothing beyond the feedback line and the missing-ingredient line.
- Notion or the Meal Planner cannot be reached: send one line saying so, nothing else.

## 6. Never

- Never write to Notion, change a meal, or tick anything.
- Never show calories or nutrition figures.
- Never add a second message in the evening.
