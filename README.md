# MealieRecipeParser

[![Mealie v2.x](https://img.shields.io/badge/Mealie-v2.x-green.svg)](https://mealie.io)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

A ChatGPT Project that converts recipes from photos, screenshots, PDF text, or URLs into **schema.org/Recipe JSON-LD** for import into [Mealie](https://mealie.io).

## What It Does

Paste a recipe URL, upload a photo of a cookbook page, or type a recipe, and the project outputs a single, valid JSON-LD object ready for Mealie import. All text is in Dutch.

Three modes:

- **Recipe mode (default).** Parses any recipe input into schema.org/Recipe JSON
- **Image mode (`/image`).** Generates a realistic food photo of the last parsed recipe
- **Description mode (`/desc`).** Writes or rewrites a short Dutch recipe description

## Example

Input: a recipe URL or photo

Output: one JSON code block

```json
{
  "@context": "https://schema.org",
  "@type": "Recipe",
  "name": "Rode linzensoep met kokosmelk",
  "description": "Romige soep met rode linzen en kokosmelk. Licht pittig met een vleugje limoen.",
  "recipeCategory": ["Soep"],
  "recipeCuisine": "Indiaas",
  "recipeYield": "4 porties",
  "prepTime": "PT15M",
  "cookTime": "PT25M",
  "totalTime": "PT40M",
  "keywords": ["tijd | 30-60", "keuken | indiaas", "dieet | vegan", "pittig | mild"],
  "recipeIngredient": [
    "1 el kokosolie",
    "1 ui, fijngesneden",
    "3 teentjes knoflook, geperst",
    "300 g rode linzen (masoor dal), afgespoeld",
    "400 ml kokosmelk",
    "1 limoen [sap]"
  ],
  "recipeInstructions": [
    {"@type": "HowToStep", "text": "Verhit de kokosolie in een grote pan op middelhoog vuur."},
    {"@type": "HowToStep", "text": "Fruit de ui 3 minuten. Voeg de knoflook toe en bak 1 minuut mee."},
    {"@type": "HowToStep", "text": "Voeg de linzen, kokosmelk en 400 ml water toe. Breng aan de kook."},
    {"@type": "HowToStep", "text": "Laat 20 minuten zachtjes koken tot de linzen zacht zijn."},
    {"@type": "HowToStep", "text": "Pureer de soep glad. Breng op smaak met limoensap, zout en peper."}
  ]
}
```

## Setup

1. Create or open a ChatGPT Project
2. Copy the contents of `system-prompt.txt` into **Project Instructions**
3. Upload all other files as **Project Files**

That's it. Start chatting with a recipe.

## How It Works

The system prompt defines the modes and output rules. The reference files contain the detailed rules for each aspect of recipe parsing:

### Recipe Structure
| File | Purpose |
|---|---|
| `categories.json` | Allowed `recipeCategory` values with keyword heuristics |
| `instructions-format.md` | Rules for `HowToStep` / `HowToSection` |
| `description-rules.md` | Rules for short recipe descriptions |
| `url-rules.md` | URL input and image extraction |

### Ingredients and Normalization
| File | Purpose |
|---|---|
| `ingredient-format.md` | Mealie ingredient parsing, notes, DB qualifiers, substitutions |
| `unit-conversions.md` | Metric conversions |
| `time-rules.md` | Time fields and ISO 8601 |

### Tags and Metadata
| File | Purpose |
|---|---|
| `tags-rules.md` | Tag/facet rules |
| `tags_whitelist_facets.json` | Whitelist for tags (cuisine, diet, time, protein, spiciness) |
| `diet-mapping.json` | schema.org `suitableForDiet` mapping |
| `cuisine-map.json` | Cuisine translation/normalization |
| `tools-list.md` | Optional schema.org `tool` recognition |

## Key Design Decisions

**Ingredient lines use two bracket types.** Square brackets `[...]` are DB qualifiers that stay part of the ingredient name (for matching against your Mealie database, e.g., `zwarte peper [gemalen]`). Round brackets `(...)` become notes in Mealie (e.g., `rode linzen (masoor dal)`).

**Tags are faceted.** Every tag follows `{type} | {value}` with a fixed whitelist. No free-form tags. This keeps filtering consistent across hundreds of recipes. Time is mandatory; cuisine, diet, protein, and spiciness are optional.

**Categories use keyword heuristics.** The `categories.json` file has priority groups and keyword rules to auto-classify recipes. Falls back to "Hoofdgerecht" when nothing matches.

**All text is Dutch.** The LLM translates foreign recipe content and normalizes everything to Dutch.

## Maintenance

Edit the specific rule file when you need to change behavior. Keep `system-prompt.txt` short; it should reference the files, not duplicate them.

Common changes:
- New categories: edit `categories.json`
- New tags: edit `tags-rules.md` + `tags_whitelist_facets.json`
- Ingredient rules: edit `ingredient-format.md`
- Time handling: edit `time-rules.md`

## Related

- [MealieSync](https://github.com/Rouzax/MealieSync): manages Mealie's ingredient, unit, label, category, tag, and tool data via REST API. Includes Dutch and French ingredient databases.

## License

[MIT](LICENSE)
