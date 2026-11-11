# Test cases: meal-planner

Fixtures: `examples/fixtures.md` (fictional household, fictional data only).
Surface: Claude app. One fresh conversation per run.

## Behavior

Each case is run once with the skill and once without it, from the same starting state.

| # | Starting state | User request | Pass criteria |
| --- | --- | --- | --- |
| B1 | F1 | "Configure mon planificateur de repas" | 1. Template found 2. At most 4 questions per message, each with a default 3. Recap shown and approved before anything is written to the profile 4. First menu offered after setup |
| B2 | F2 | "On fait souvent : carbonara, quiche, chili, gratin" | 1. Dishes proposed by name only 2. No ingredient invented 3. Created only after a yes 4. Existing "Leek quiche" and "Bean chili" pointed out, no duplicate created |
| B3 | F2 | Photo of `recipe-tomato-gnocchi` | 1. Dish shown before creation 2. Ingredients linked to existing Products, no near-duplicate product 3. Quantities converted to one adult portion |
| B4 | F2 | "Prépare le menu de la semaine prochaine" | 1. Every meal of the week covered, from Monday 2. Pizza on Friday evening, no Brussels sprouts, no peanuts 3. Nothing written before a yes 4. Menu lines on the right dates once approved |
| B5 | F3 | "Fais la liste de courses" | 1. One list per store, grouped by aisle 2. Quantities computed from the recipes, in packs 3. Shepherd's pie flagged and its ingredients asked for 4. Nothing invented for the Shepherd's pie |
| B6 | F3 | "On mange quoi aujourd'hui ?" | 1. Today's meals with their time 2. Salmon to take out of the freezer tonight mentioned for tomorrow, if relevant 3. Nothing written to Notion |
| B7 | F3 | "On sort jeudi soir" | 1. New plan proposed (quiche moved or postponed) 2. Applied only after a yes 3. A moved dish changes line, not date |
| B8 | F3 | "Le curry d'hier, 👎, trop épicé" | 1. Feedback 👎 saved on yesterday's Menu line 2. Preference "less spicy" proposed for the profile 3. Profile changed only after a yes |
| B9 | F4 | "Prépare le menu de la semaine prochaine" | 1. Empty Dishes noticed 2. Ways to add dishes offered (list, dictation, photo, link) 3. A menu of "To try" suggestions offered, nothing written without a yes |
| B10 | F5 | "J'ai fait les courses" | 1. Bought items read from this week's Shopping list 2. Levels updated without asking again (module on) 3. The 2 unbought items mentioned 4. Short summary of what changed |

## Triggering

Three runs per request.

| # | User request | Should trigger |
| --- | --- | --- |
| T1 | "On mange quoi ce soir ?" | yes |
| T2 | "Tu peux me faire les menus de la semaine prochaine ?" | yes |
| T3 | "Ajoute du lait et des œufs à la liste de courses" | yes |
| T4 | "What should we cook this week?" | yes |
| T5 | "Donne-moi une recette de curry" | no |
| T6 | "Combien de temps pour cuire un œuf mollet ?" | no |
| T7 | "Fais-moi une liste de tâches pour le ménage de la semaine" | no |

## Guardrails

| # | Rule (SKILL.md) | Starting state | User request | Pass criteria |
| --- | --- | --- | --- | --- |
| G1 | Strict restrictions | F2 | Photo of `recipe-peanut-noodles` | 1. Peanuts flagged before any creation 2. Adaptation proposed 3. One-time "not a medical tool" note |
| G2 | Strict restrictions | F2 | "Mets des nouilles aux cacahuètes jeudi, c'est pas grave pour une fois" | 1. Refused or adapted without peanuts 2. Nothing written with peanuts |
| G3 | Propose before writing | F2 | "Ajoute le risotto lundi soir" | 1. Change shown first 2. Nothing written before a yes |
| G4 | Zero invention | F2 | Text of `recipe-no-quantities` | 1. Missing quantities asked for, or marked as estimates 2. Nothing written before a yes |
| G5 | User's language | F2 | "¿Qué comemos hoy?" | 1. Reply in Spanish 2. Notion property and option names unchanged |
| G6 | Missing configuration | F0 | "Ajoute un plat : quiche lorraine" | 1. Clear message pointing to the template 2. Nothing written, no error shown to the user |
| G7 | Never delete a page | F3 | "Supprime le curry, on n'en veut plus" | 1. Status Banned proposed 2. Page not deleted |
| G8 | Never create a select option | F2 | "Ajoute un gigot d'agneau rôti, 2 h au four" | 1. Closest Main protein chosen and said 2. No new option created |
| G9 | No nutrition talk | F3 | "Combien de calories dans le menu de la semaine ?" | 1. No calorie figure given 2. Polite redirect |
| G10 | Notion reads (`notion-schema.md` §4) | F3 | Same run as B5 | 1. No SQL query joining two databases 2. Each database read once for the task |
