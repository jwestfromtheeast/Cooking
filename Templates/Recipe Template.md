<%*
// ── Recipe Template (Templater) ─────────────────────────────────
// Prompts for metadata, builds frontmatter + tags, and files the
// note into Recipes/<Cuisine>/. Esc on any prompt uses a default.
let title = tp.file.title;
if (title.startsWith("Untitled")) {
  title = (await tp.system.prompt("Recipe name")) ?? "New Recipe";
}
const cuisines = ["American","Chinese","Filipino","French","German","Greek","Indian","Indonesian","Italian","Japanese","Korean","Lebanese","Malaysian","Mexican","Moroccan","Singaporean","Spanish","Thai","Turkish","Vietnamese","Other…"];
let cuisine = await tp.system.suggester(cuisines, cuisines, false, "Cuisine (country)");
if (!cuisine || cuisine === "Other…") {
  cuisine = (await tp.system.prompt("Cuisine / country (Title Case, used as folder name)")) ?? "Other";
}
const courses = ["main","side","appetizer","soup","salad","dessert","breakfast","snack","drink","sauce"];
const course = (await tp.system.suggester(courses, courses, false, "Course")) ?? "main";
const types = ["pasta","soup","stew","curry","stir-fry","rice","noodles","salad","sandwich","roast","fish","grill","baked-goods","dessert","sauce","other"];
const type = (await tp.system.suggester(types, types, false, "Dish type (for #type/ tag)")) ?? "other";
const diffs = ["easy","medium","hard"];
const difficulty = (await tp.system.suggester(diffs, diffs, false, "Difficulty")) ?? "medium";
const prep = parseInt((await tp.system.prompt("Prep time (minutes)", "15")) ?? "0") || 0;
const cook = parseInt((await tp.system.prompt("Cook time (minutes)", "30")) ?? "0") || 0;
const total = prep + cook;
const servings = (await tp.system.prompt("Servings", "4")) ?? "4";
const source = (await tp.system.prompt("Source (e.g. NYT Cooking, Serious Eats)", "")) ?? "";
const url = (await tp.system.prompt("Source URL", "")) ?? "";
const ingRaw = (await tp.system.prompt("Key ingredients, comma-separated (2–4, for #ingredient/ tags)", "")) ?? "";
const slug = s => s.trim().toLowerCase().replace(/\s+/g, "-");
const cuisineTag = slug(cuisine);
const ingTags = ingRaw.split(",").map(slug).filter(x => x).map(x => `  - ingredient/${x}`).join("\n");
const sourceLine = url ? `[${source || "Link"}](${url})` : (source || "—");
if (title !== tp.file.title) { await tp.file.rename(title); }
await tp.file.move(`Recipes/${cuisine}/${title}`);
-%>
---
aliases: []
source: <% source %>
url: <% url %>
cuisine: <% cuisineTag %>
course: <% course %>
difficulty: <% difficulty %>
prep_time: <% prep %>
cook_time: <% cook %>
total_time: <% total %>
servings: <% servings %>
rating: 
tried: false
favorite: false
date_added: <% tp.date.now("YYYY-MM-DD") %>
last_made: 
tags:
  - recipe
  - cuisine/<% cuisineTag %>
  - type/<% type %>
  - difficulty/<% difficulty %>
<% ingTags %>
---

# <% title %>

> [!info]+ At a Glance
> **Prep:** <% prep %> min · **Cook:** <% cook %> min · **Total:** <% total %> min
> **Serves:** <% servings %> · **Difficulty:** <% difficulty %> · **Source:** <% sourceLine %>

> [!note]- Notes
> - 

## Ingredients

#ingredients
- [ ] 

## Directions

1. 

## To Serve

- 

## Variations & Substitutions

- 

## Log

| Date | Rating | Notes |
| ---- | ------ | ----- |
|      |        |       |
