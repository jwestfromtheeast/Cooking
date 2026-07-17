---
tags:
  - meta
---

# 🍳 Recipe Library

See [[Tags & Conventions]] for how everything is organized · Browse everything in [[Recipe Browser]]

## 📊 At a glance

```dataview
TABLE WITHOUT ID
  length(rows) as "Recipes",
  length(filter(rows, (r) => r.tried = true)) as "Tried",
  length(filter(rows, (r) => r.favorite = true)) as "Favorites"
FROM "Recipes"
WHERE contains(tags, "recipe") OR contains(file.tags, "#recipe")
GROUP BY true
```

## ⭐ Favorites

```dataview
TABLE WITHOUT ID file.link as Recipe, cuisine as Cuisine, total_time + " min" as Time, rating as "★"
FROM "Recipes"
WHERE favorite = true
SORT rating DESC
```

## ⚡ Quick meals (≤ 35 min)

```dataview
TABLE WITHOUT ID file.link as Recipe, cuisine as Cuisine, course as Course, total_time + " min" as Time
FROM "Recipes"
WHERE total_time <= 35
SORT total_time ASC
```

## 🧪 To try

```dataview
TABLE WITHOUT ID file.link as Recipe, cuisine as Cuisine, difficulty as Difficulty, total_time + " min" as Time
FROM "Recipes"
WHERE tried != true
SORT date_added DESC
```

## 🆕 Recently added

```dataview
TABLE WITHOUT ID file.link as Recipe, cuisine as Cuisine, date_added as Added
FROM "Recipes"
SORT date_added DESC
LIMIT 10
```

## 🍽️ Recently made

```dataview
TABLE WITHOUT ID file.link as Recipe, last_made as "Last Made", rating as "★"
FROM "Recipes"
WHERE last_made
SORT last_made DESC
LIMIT 10
```
