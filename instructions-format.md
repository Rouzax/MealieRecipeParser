# recipeInstructions (Mealie-compat) + behapbare stappen

## Hard format
- recipeInstructions = array van objecten met exact:
  {"@type":"HowToStep","text":"..."}
- GEEN HowToDirection en GEEN extra velden per stap.

## Behapbare stappen
- Richtlijn: 1–2 zinnen per stap.
- Splits altijd bij:
  - nieuwe handeling (snijden/mengen/bakken/koken/oven),
  - nieuw ingrediënt toevoegen,
  - nieuwe pan/oven/temperatuur,
  - expliciete tijd/wachtmoment.

## Tools en tijden
- Als je tools of tijden wilt vermelden: zet ze in de staptekst (geen extra step-velden).
- Voeg niets toe dat niet in de bron staat.

## Secties met HowToSection (schema.org)
Als de bron duidelijke sectiekoppen heeft, gebruik dan `HowToSection` zodat de structuur behouden kan blijven.

Structuur:
- `recipeInstructions` is een array van:
  - `{"@type":"HowToStep","text":"..."}`
  - of `{"@type":"HowToSection","name":"...","itemListElement":[{"@type":"HowToStep","text":"..."}]}`

Regels:
- Max 2–6 secties per recept (alleen als het echt structuur geeft).
- Binnen een sectie blijven stappen behapbaar (1–2 zinnen).
- Gebruik **geen** extra velden in HowToStep (alleen `@type` en `text`).
- Gebruik **geen** losse kop-stappen als je HowToSection gebruikt (voorkomt dubbele koppen).
