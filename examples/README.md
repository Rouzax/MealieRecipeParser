# Examples

Real input/output pairs from the MealieRecipeParser ChatGPT Project.

## Examples

| # | Input | Recipe | Key features shown |
|---|---|---|---|
| [01](01-url-ottolenghi-aubergine.md) | URL | Geblakerde aubergine met feta en harissa-olie | URL + image extraction, `[vers]` qualifier, `dieet` tag, `pittig | medium` |
| [02](02-url-ottolenghi-ribs.md) | URL | Rokerige varkensribben met groene saus | Multiple categories (BBQ + Hoofdgerecht), `[gemalen]`/`[blad]` qualifiers, `eiwit` tag, foreign name in `(...)` |
| [03](03-photo-cookbook-kip.md) | Cookbook photo | Kip met chilipeper en knoflook | Photo input, page reference removal, `[gedroogd]` qualifier, `(methi)` foreign name, `keuken | indiaas` |

## Feature Coverage

| Feature | 01 | 02 | 03 |
|---|---|---|---|
| URL input | x | x | |
| Photo input | | | x |
| Image extraction from page | x | x | |
| `[vers]` qualifier | x | | |
| `[gemalen]` qualifier | | x | |
| `[gedroogd]`/`[blad]` qualifier | | x | x |
| `(...)` foreign ingredient name | | x | x |
| `(...)` optional/notes | x | | x |
| Page reference removal | | | x |
| `dieet` tag | x | | |
| `eiwit` tag | | x | x |
| `keuken` tag | | | x |
| `pittig` tag | x | x | x |
| Multiple categories | | x | |
| Generated `/image` photo | x | x | x |

## How to Read the Examples

Each example shows:

1. **Input.** What you paste or upload into the ChatGPT Project
2. **Output.** The JSON-LD the parser produces
3. **What to notice.** Annotations explaining which rules were applied
4. **Generated image.** The food photo from `/image` mode
