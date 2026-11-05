# Feedback, changes of plan, learning

Contents: 1. What was eaten · 2. Dishes evolve · 3. Changes of plan · 4. Learning · 5. Never

## 1. What was eaten

When the user says what they ate or how it was, the message is the request: write it, then confirm.

1. **Find the Menu line**: date and meal. If it is ambiguous ("the quiche"), take the most recent and say so.
2. **Update** what the user said:
   - Status: Cooked, Leftovers, Postponed or Skipped;
   - Feedback: 👍, 😐, 👎;
   - Note: their words, in a few words ("too dry", "double the sauce");
   - Rating on the dish: only if they give one.
3. **Something else was eaten**: put that dish on the line (Status Cooked), so the history is true. If it is not in Dishes, write it in the Note and offer to add it (`recipe.md`).
4. **Stock module on**: a Cooked line lowers the levels (`stock.md` section 4).
5. **Confirm in one line**, without repeating everything. Then sections 2 and 4 if they apply.

Several meals in one message: update them all in one go.

## 2. Dishes evolve

Propose, never apply alone:

| What happened | Propose |
| --- | --- |
| 👍 on a To try dish | Status Approved |
| Two 👍 in a row on an Approved dish | Status Favorite |
| 👎 | Ask in one question: the dish, or just that day? The dish: Banned, or an adaptation (`recipe.md` section 7). That day: nothing |
| "Not enough", "too much pasta" | Change the Quantity of the Dish ingredients lines concerned (`recipe.md` section 7) |
| A step that went wrong, a tip | Edit the page body |

## 3. Changes of plan

Triggers: "we're eating out tonight", "not in the mood for that", "no cream left", "guests on Saturday", "office day on Thursday after all".

1. Understand the constraint, with one question at most.
2. Propose **one** clear change, factual tone: "Tonight → Pasta carbonara (planned Thursday); Thursday → Leek quiche (the leeks keep until then). OK?"
3. Wait for the yes, apply, confirm in one line.
4. Write the reason in the Note of each line changed ("Moved: eating out").

**How to move a dish.** Menu lines stay on their date and meal: change the Dish of the lines, never their Date. A dish that leaves the week without a new day: write "Postponed: <dish>" in the Note of the line that replaced it; the next weekly plan brings it back.

**Rules**

- Dish refused tonight: bring forward a dish planned later in the week, preferably one whose ingredients are already at home. The refused dish takes its place, or is postponed.
- Eating out: that line becomes Skipped and keeps its Dish. If its fresh products would be lost, propose moving it to a close day in place of a dish that keeps better.
- Lunchbox day added: the dinner before becomes a dish tagged Good for leftovers, with Extra for lunchbox and one more appetite in Servings; the lunch line becomes Lunchbox, Note "From <dish>".
- Guests: raise Servings by their appetites; check the dish suits a table of guests and their restrictions if the user gives them.
- Missing ingredient: stock module on, set it to Out. Then, in this order: a simple substitute from what is at home, a swap with another day, or adding it to the shopping list (`shopping.md` section 10).
- The week's rules still apply: rituals, strict restrictions, season, time limits, not the same dish two days in a row.

## 4. Learning

The profile improves when the user says something lasting. Propose, then write after the yes.

| The user says | Where it goes |
| --- | --- |
| A new strict restriction ("I'm allergic to nuts") | Section "Never", right away, with the medical disclaimer; check planned dishes and flag any that contain it |
| A new taste ("my partner doesn't like salmon") | The matching section (Dislikes, Likes, Protein habits…) and one Journal line |
| A rule ("Wednesday evenings must be quick") | The matching section (Time, Meals, Rituals…), else Free rules, and one Journal line |
| A craving for now ("we're into lamb's lettuce") | Journal only, with an end date |
| A repeated pattern you notice (same day often skipped, a dish always 👎, quantities often corrected) | Propose a rule; write it only if the user agrees |

**Journal format**: one line appended at the end of the Journal section.

```
2026-10-14: Wednesday dinner must take under 30 min (sport).
2026-10-11: until 2026-11-30, lamb's lettuce as a side when possible.
```

- For a craving, ask "until when?". Without an answer, use 4 weeks and say so.
- A product mentioned (lamb's lettuce) must exist in Products; create it if needed.
- A new rule that contradicts the profile: ask which one wins before writing.
- Change only the line concerned. Never rewrite other sections.

## 5. Never

- Never apply a change of plan, a dish status or a profile change without the user's yes.
- Never delete a Menu line or a dish: use Skipped, Postponed, Banned.
- Never show calories, nutrition figures, or talk about weight.
