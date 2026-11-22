# Recipes

My recipes, bake logs, diary and baking references. This repo is the content behind
[Bake Book](https://tomstuder.github.io/baker-app/). The app reads these files and saves edits
back here as commits. You can also edit any file by hand on GitHub or locally.

## Layout

```
config.yml                          categories for each section
home.md                             home page: bio, photos, featured recipes, social links
images/home/                        home page photos
recipes/<slug>/recipe.md            one folder per recipe
recipes/<slug>/bakes/<date>.md      bake log entries (coming soon)
recipes/<slug>/images/              photos
diary/<date>-<slug>.md              diary posts (coming soon)
references/techniques/<slug>.md     how-tos and technique notes
```

`<slug>` is the title in lowercase with hyphens, e.g. `sourdough-banana-bread`.

## Recipe format

Each `recipe.md` starts with a header block between `---` lines (YAML), followed by the
write-up in Markdown.

```yaml
---
title: Sourdough Banana Bread
category: Quick breads & muffins    # one of the categories in config.yml
tags: [banana, sourdough-discard]   # any number of free-form tags
status: tested                      # draft | testing | tested
created: 2026-05-23
yield: 2 loaves (8×4" pans)         # optional
servings: 10–12 slices              # optional
time: { prep: 15 min, bake: 45–60 min }   # optional
oven: 350°F                         # optional; the app shows °F and °C
equipment: [Loaf pans, Whisk]       # optional
ingredients:
  - group: Dry                      # groups are optional; use one group for a plain list
    note: Optional note for the group
    items:
      - { name: Flour, amount: 2 cups, grams: 240, pct: 100, flour: true }
      - { name: Large eggs, amount: "2", grams: 100, pct: 41.7, water: 75, estimated: true }
      - { name: Sourdough starter, grams: 125, pct: 52.1, hydration: 100 }
---
```

Ingredient fields:

| Field | Meaning |
|---|---|
| `name` | Required. |
| `amount` | The amount as written, e.g. `1 cup` or `3 medium`. Optional. |
| `grams` | Weight in grams. **This is the source of truth** for scaling and baker's %. |
| `pct` | Baker's percentage: grams ÷ total flour (the `flour: true` items) × 100. The app recalculates it when saving. |
| `flour: true` | Counts toward the 100% flour base. |
| `hydration` | Marks a preferment (levain, starter, poolish, biga) and gives its hydration %. Its flour and water count toward overall hydration but not the flour base. |
| `water` | Water content as a % of the ingredient's weight, e.g. milk 87, eggs 75, butter 16. Counts toward overall hydration. |
| `estimated: true` | The weight is an estimate (e.g. 1 large egg ≈ 50 g). |
| `note` | Short note, e.g. `mashed` or `all-purpose or bread flour`. |

Everything after the header is regular Markdown. Typical sections are `## Method`,
`## Baker's percentages`, `## Storage` and `## Notes`.

## License

[CC0 1.0](LICENSE): public domain.
