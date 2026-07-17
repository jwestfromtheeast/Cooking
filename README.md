# 🍳 Cooking

A personal recipe library, built as an [Obsidian](https://obsidian.md/) vault.

Recipes live in `Recipes/<Cuisine>/`, one markdown file each, with structured YAML frontmatter (cuisine, course, difficulty, times, servings, rating) and nested tags (`#cuisine/japanese`, `#ingredient/chicken`, `#type/soup`, `#difficulty/easy`) for searching and filtering.

Start at **Home.md** — a Dataview-powered dashboard with favorites, quick meals, a to-try list, and recently added/made. **Meta/Recipe Browser.md** groups everything by cuisine, course, difficulty, and ingredient. **Meta/Tags & Conventions.md** documents the full schema and tag taxonomy.

New recipes are created with **Templates/Recipe Template.md**, a [Templater](https://github.com/SilentVoid13/Templater) template that prompts for metadata, builds the frontmatter and tags, and files the note into the right cuisine folder automatically.

Requires the Dataview and Templater community plugins (settings included in `.obsidian/`).
