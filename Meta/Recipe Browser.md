---
tags:
  - meta
---

# 📖 Recipe Browser

Every recipe, grouped different ways. New cuisines/types appear automatically.

## By cuisine

```dataview
TABLE rows.file.link as Recipes, length(rows) as Count
FROM "Recipes"
GROUP BY cuisine as Cuisine
SORT Cuisine ASC
```

## By course

```dataview
TABLE rows.file.link as Recipes, length(rows) as Count
FROM "Recipes"
GROUP BY course as Course
SORT Course ASC
```

## By difficulty

```dataview
TABLE rows.file.link as Recipes, length(rows) as Count
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

## By key ingredient

```dataview
TABLE rows.file.link as Recipes, length(rows) as Count
FROM "Recipes"
FLATTEN file.etags as t
WHERE startswith(t, "#ingredient/")
GROUP BY t as Ingredient
SORT Ingredient ASC
```

Recipes appear once per key ingredient here — that's expected. For one-off searches use the search pane: `tag:#ingredient/chicken`.

## Components by type

```dataview
TABLE rows.file.link as Components, length(rows) as Count
FROM "Components"
FLATTEN file.etags as t
WHERE startswith(t, "#type/")
GROUP BY t as Type
SORT Type ASC
```
