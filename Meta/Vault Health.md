---
tags:
  - meta
---

# 🩺 Vault Health

Lint checks for the recipe schema. Every table below should be **empty** — anything listed needs fixing.

## Rating out of range (must be 1–10)

```dataview
TABLE rating as Rating
FROM "Recipes"
WHERE rating != null AND (rating < 1 OR rating > 10)
```

## Tried but never rated

```dataview
TABLE last_made as "Last Made"
FROM "Recipes"
WHERE tried = true AND rating = null
```

## Rated but not marked tried

```dataview
TABLE rating as Rating
FROM "Recipes"
WHERE rating != null AND tried != true
```

## Tried but no last_made date

```dataview
TABLE rating as Rating
FROM "Recipes"
WHERE tried = true AND last_made = null
```

## Missing core metadata

```dataview
TABLE cuisine as Cuisine, course as Course, difficulty as Difficulty, total_time as "Total (min)"
FROM "Recipes"
WHERE cuisine = null OR course = null OR difficulty = null OR total_time = null OR servings = null
```

## Missing required tags

```dataview
TABLE file.etags as Tags
FROM "Recipes"
WHERE !contains(file.etags, "#recipe")
  OR none(file.etags, (t) => startswith(t, "#cuisine/"))
  OR none(file.etags, (t) => startswith(t, "#type/"))
  OR none(file.etags, (t) => startswith(t, "#difficulty/"))
  OR none(file.etags, (t) => startswith(t, "#ingredient/"))
```
