---
tags:
  - meta
---

# 🎲 What Should I Eat?

Click any button to (re)roll a random recipe matching that constraint. Ties are broken by pure chance, as the universe intended.

```dataviewjs
const all = dv.pages('"Recipes"').array();
const pick = arr => arr[Math.floor(Math.random() * arr.length)];
const row = (label, arr) => {
  const div = this.container.createEl("div");
  div.style.margin = "0.4em 0";
  const btn = div.createEl("button", { text: "🎲 " + label });
  btn.style.marginRight = "0.6em";
  const out = div.createEl("span");
  const roll = () => {
    out.empty();
    if (!arr.length) { out.setText("(no matches yet)"); return; }
    const p = pick(arr);
    const a = out.createEl("a", { text: p.file.name, cls: "internal-link" });
    a.dataset.href = p.file.path;
    a.onclick = () => app.workspace.openLinkText(p.file.path, "", false);
    out.createEl("span", { text: `  (${p.cuisine ?? "?"} · ${p.total_time ?? "?"} min · ${p.difficulty ?? "?"})` });
  };
  btn.onclick = roll;
  roll();
};
row("Anything", all);
row("Quick (≤35 min)", all.filter(p => p.total_time <= 35));
row("Something new", all.filter(p => p.tried !== true));
row("A favorite", all.filter(p => p.favorite === true));
row("Vegetarian", all.filter(p => (p.file.etags ?? []).map(String).includes("#diet/vegetarian")));
row("Soup or rice bowl", all.filter(p => { const t = (p.file.etags ?? []).map(String); return t.includes("#type/soup") || t.includes("#type/rice"); }));
```

## By ingredient on hand

Type in search (`Ctrl+Shift+F`): `path:Recipes "chicken"` for full-text, or `tag:#ingredient/chicken` for key-ingredient matches. Or just ask Claude — "what can I make with mushrooms and rice?"
