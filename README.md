# Recipes

My recipes, bake logs, journal and baking references. This repo is the content behind
[Tom Studer's Bakes](https://kitchen.tomstuder.com/). The app reads these files and saves edits
back here as commits. You can also edit any file by hand on GitHub or locally.

## Layout

```
config.yml                          categories for each section
home.md                             home page: bio, photos, featured recipes, social links
images/home/                        home page photos
recipes/<slug>/recipe.md            one folder per recipe
recipes/<slug>/bakes/<date>.md      bake log entries, one file per bake
recipes/<slug>/images/              photos
diary/<date>-<slug>.md              journal posts (the folder is still called diary)
diary/images/                       journal photos
references/techniques/<slug>.md     how-tos and technique notes (photos in references/techniques/images/)
references/glossary.yml             glossary terms
references/library.yml              links, books, videos, articles and uploaded files
references/files/                   uploaded files (PDFs etc.)
references/conversions.yml          cup/tbsp/tsp weights for the converter
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

## Bake format

Each bake is its own file in the recipe's `bakes/` folder, named by date (plus the title, if any),
e.g. `recipes/sourdough-base/bakes/2026-11-23-higher-hydration.md`.

```yaml
---
date: 2026-11-23
title: Higher hydration              # optional
rating: 4                            # 1–5, optional
batch: 2 loaves (900 g each)         # optional
changes:                             # what was different from the recipe
  - Water 75% → 78%
temps: { kitchen: 72°F, dough: 78°F, oven: 475°F }   # any of these, optional
timeline:
  - { time: "08:00", step: Build levain }
  - { time: "20:00", step: "Shape, then into the fridge" }
photos:                              # relative to this file; photos live in the recipe's images/ folder
  - ../images/2026-11-23-crumb.jpg
---

Notes in Markdown: crumb, crust, flavor, what to try next time.
```

**Quoting:** inside `{ … }` on one line, put text that contains a comma or a colon in double quotes
(`"Shape, then into the fridge"`), and always quote times like `"08:00"`. The app does this
automatically when it saves.

## Journal post format

One file per post in `diary/`, named by date and title, e.g. `diary/2026-11-21-first-rye-loaf.md`.

```yaml
---
title: First rye loaf
date: 2026-11-21
category: Experiment                 # one of the journal categories in config.yml
tags: [rye, sourdough]
image: images/2026-11-21-rye.jpg     # optional cover photo, relative to this file
related:                             # optional links shown at the end of the post
  - sourdough-base                   # a recipe (its folder name)
  - sourdough-base/2026-11-20-higher-hydration   # a specific bake
---

Text in Markdown. Photos can go anywhere in the text: ![Crumb](images/2026-11-21-crumb.jpg)
```

## References formats

**Techniques** (`references/techniques/<slug>.md`): a header with `title`, optional `summary`,
`tags`, `status: draft` (leave it out once published), `created` and a cover `image`, then the
write-up in Markdown.

**Glossary** (`references/glossary.yml`), kept in A–Z order:

```yaml
terms:
  - term: Autolyse
    definition: Resting just the flour and water… (Markdown allowed)
```

**Library** (`references/library.yml`), shown in this order. `type` is website, video, book,
article or file:

```yaml
items:
  - type: book
    title: Flour Water Salt Yeast
    author: Ken Forkish
  - type: website
    title: Ingredient weight chart
    url: https://www.kingarthurbaking.com/learn/ingredient-weight-chart
    tags: [conversions]
  - type: file
    title: Starter feeding schedule
    file: files/2026-11-23-starter-schedule.pdf   # relative to references/
```

**Conversions** (`references/conversions.yml`): the weight of one `cup`, `tbsp` or `tsp`:

```yaml
volume:
  - { name: All-purpose flour, unit: cup, grams: 120 }
```

## License

[CC0 1.0](LICENSE): public domain.
