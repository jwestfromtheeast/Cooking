---
tags:
  - meta
---

# 📅 Meal Plan

Fill in links per night — recipes autocomplete when you type `[[`. Ask Claude to draft a week from constraints ("plan 4 weeknight dinners, ≤45 min, one vegetarian, nothing I made last week") — the vault metadata makes that a one-liner.

## Week of 

| Day | Recipe | Notes |
| --- | ------ | ----- |
| Mon |        |       |
| Tue |        |       |
| Wed |        |       |
| Thu |        |       |
| Fri |        |       |
| Sat |        |       |
| Sun |        |       |

## Shopping list

- [ ] 

## On deck (untried, quickest first)

```dataview
TABLE WITHOUT ID file.link as Recipe, cuisine as Cuisine, total_time + " min" as Time, difficulty as Difficulty
FROM "Recipes"
WHERE tried != true
SORT total_time ASC
LIMIT 8
```
