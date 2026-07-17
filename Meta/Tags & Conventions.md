---
tags:
  - meta
---

# Tags & Conventions

The single source of truth for how recipes in this vault are structured. Every recipe follows the schema below so Dataview queries, dashboards, and search stay reliable.

## Folder layout

```
Cooking/
├── Home.md                  ← dashboard (start here)
├── What Should I Eat.md     ← random-pick buttons with constraints
├── Meal Plan.md             ← weekly planner
├── Components/              ← reusable sauces, marinades, stocks (tagged #component, not #recipe)
├── Recipes/
│   ├── Italian/
│   ├── Japanese/
│   ├── Singaporean/
│   ├── Thai/
│   ├── <Country>/           ← one folder per country-level cuisine, Title Case
│   └── Other/               ← fusion, unknown, or uncategorizable
├── Templates/
│   └── Recipe Template.md   ← Templater-powered, prompts on creation
└── Meta/                    ← docs & index notes (this file, Recipe Browser)
```

## Frontmatter properties

Every recipe has these properties. Numeric times (minutes) make sorting and "quick meals" queries work — don't write "30 min", write `30`.

| Property     | Type    | Example                  | Notes                                    |
| ------------ | ------- | ------------------------ | ---------------------------------------- |
| `aliases`    | list    | `[Miso Cod]`             | Alternate names for quick switcher       |
| `source`     | text    | `NYT Cooking`            | Publication or cookbook title ("The Wok", "Salt Fat Acid Heat") |
| `author`     | text    | `Eric Kim`               | Recipe author; "X, adapted by Y" is fine. Search: `["author":Kim]` or Dataview `contains(author, "Kim")` |
| `url`        | text    | `https://…`              | Link to original                         |
| `cuisine`    | text    | `japanese`               | lowercase, hyphenated                    |
| `course`     | text    | `main`                   | main, side, appetizer, soup, salad, dessert, breakfast, snack, drink, sauce |
| `difficulty` | text    | `easy`                   | easy, medium, hard                       |
| `prep_time`  | number  | `15`                     | minutes                                  |
| `cook_time`  | number  | `30`                     | minutes                                  |
| `total_time` | number  | `45`                     | minutes, incl. marinating etc.           |
| `servings`   | number  | `4`                      |                                          |
| `rating`     | number  | `8`                      | **1–10**, leave blank until tried. Rough guide: 9–10 house staple, 7–8 make again, 5–6 fine once, ≤4 skip. [[Vault Health]] flags out-of-range values. |
| `tried`      | checkbox| `true`                   | have you actually made it?               |
| `favorite`   | checkbox| `false`                  | greatest-hits flag                       |
| `date_added` | date    | `2026-07-16`             |                                          |
| `last_made`  | date    | `2026-07-16`             | enforced as a date (picker in Properties panel); update after cooking |
| `tags`       | list    | see below                |                                          |

## Tag taxonomy (nested)

All tags are lowercase and hyphenated. Every recipe gets `#recipe` plus tags from these namespaces:

| Namespace      | Required | Examples                                                    |
| -------------- | -------- | ----------------------------------------------------------- |
| `cuisine/`     | yes      | Country-level: `cuisine/japanese`, `cuisine/italian`, `cuisine/singaporean`, `cuisine/thai`; use `cuisine/other` for fusion/unknown |
| `type/`        | yes      | `type/pasta`, `type/soup`, `type/rice`, `type/curry`, `type/stir-fry`, `type/salad`, `type/roast`, `type/fish`, `type/baked-goods`, `type/dessert`, `type/sauce` |
| `difficulty/`  | yes      | `difficulty/easy`, `difficulty/medium`, `difficulty/hard`   |
| `ingredient/`  | yes      | 2–4 *key* ingredients only: `ingredient/chicken`, `ingredient/miso`, `ingredient/mushroom` |
| `method/`      | optional | `method/broil`, `method/grill`, `method/slow-cook`, `method/one-pot`, `method/no-cook` |
| `diet/`        | optional | `diet/vegetarian`, `diet/vegan`, `diet/gluten-free`, `diet/dairy-free` |
| `season/`      | optional | `season/summer`, `season/holiday`                           |

Rules of thumb: tag the ingredients you'd *search by* ("what can I make with mushrooms?"), not the whole shopping list. Cuisine, course, and difficulty live in **both** properties (for tables/sorting) and tags (for the tag pane and graph) — the template handles this automatically.

## Body structure

Recipes use `#` for the title and `##` for sections, in this order: **At a Glance** callout → **Notes** callout → **Ingredients** (checkboxes, under an `#ingredients` inline tag so checklist plugins can build shopping lists) → **Directions** → **To Serve** → **Variations & Substitutions** → **Log** (freeform table of dates made, ratings, and tweaks — nothing queries it, so write whatever's useful; just remember the `last_made` and `rating` *properties* are what feed the dashboards).

## Adding a recipe

1. Hotkey/command: **Templater: Create new note from template** → `Recipe Template`.
2. Answer the prompts (name, cuisine, type, difficulty, times, key ingredients…).
3. The note auto-fills its frontmatter, tags itself, and moves into `Recipes/<Cuisine>/`.
4. Paste in ingredients and directions. Done — it appears on [[Home]] automatically.
