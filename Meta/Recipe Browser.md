---
tags:
  - meta
---

# 📖 Recipe Browser

Every recipe, grouped different ways. New cuisines/types appear automatically.

## By cuisine

```dataview
TABLE WITHOUT ID rows.file.link as Recipes, length(rows) as Count
FROM "Recipes"
GROUP BY cuisine as Cuisine
SORT Cuisine ASC
```

## By course

```dataview
TABLE WITHOUT ID rows.file.link as Recipes, length(rows) as Count
FROM "Recipes"
GROUP BY course as Course
SORT Course ASC
```

## By difficulty

```dataview
TABLE WITHOUT ID rows.file.link as Recipes, length(rows) as Count
FROM "Recipes"
GROUP BY difficulty as Difficulty
SORT Difficulty ASC
```

## Full table

```dataview
TABLE cuisine as Cuisine, course as Course, difficulty as Diff, total_time + " min" as Time, servings as Serves, rating as "★", tried as Tried
FROM "Recipes"
SORT cuisine ASC, file.name ASC
```

## Search by ingredient

Use the tag pane or search, e.g. `tag:#ingredient/chicken`. Ingredient tags in use:

```dataview
TABLE WITHOUT ID rows.file.link as Recipes
FROM "Recipes"
FLATTEN file.etags as t
WHERE startswith(t, "#ingredient/")
GROUP BY t as Ingredient
SORT Ingredient ASC
```
