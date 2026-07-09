# Mealie Tags Rules (facets)

## Doel
Tags zijn bedoeld om recepten **consistent te filteren** met een **kleine, stabiele whitelist**.
Geen ingredient-tags en geen vrije “vergaarbak”-tags.

## Categories vs Tags
- **Categories**: moment/gang/soort recept (ontbijt, lunch, hoofdgerecht, dessert, borrel, soep, salade, etc.).
- **Tags**: alleen facetten die dwars door categories heen filteren.

## Tag-formaat (verplicht)
Elke tag volgt exact:

`{type} | {waarde}`

Conventies:
- alles **lowercase**
- exact **1 spatie** vóór en na `|`
- geen dubbele spaties
- geen samengestelde tags (dus niet `keuken | koreaans, pittig, aziatisch`)

## Toegestane types (whitelist)
We staan alleen deze types toe:
- `keuken | …`
- `dieet | …`
- `tijd | …`
- `eiwit | …` (optioneel; alleen bij dierlijke hoofd-eiwitbron)
- `pittig | …` (optioneel; 1 niveau per recept)

Alles buiten deze types wordt verwijderd.

## tijd (verplicht, exact 1 per recept)
Toegestane waarden:
- `tijd | 0-30`
- `tijd | 30-60`
- `tijd | 60+`

Regel:
- kies op basis van **totale tijd** (prep + cook), niet per stap.

## dieet (optioneel, 0–3 per recept)
Voor dieet/allergie-achtig filteren (alleen waarden die in de whitelist staan).

## keuken (optioneel, meestal max 1 per recept)
Richtlijnen:
- kies de **dominante** keuken/stijl.
- micro-keukens mappen naar de dichtstbijzijnde brede keuken.
  Voorbeeld: `bengaals` → `keuken | indiaas`.
- voeg een nieuwe keuken pas toe aan de whitelist als je er **minstens 2–3 recepten** voor hebt.

## eiwit (optioneel, max 1 per recept; alleen dierlijk)
Doel: filteren op hoofd-eiwitbron bij niet-vegetarische recepten.
Regels:
- alleen gebruiken als er een **duidelijke dierlijke** hoofdcomponent is
- niet gebruiken bij vegetarisch/vegan (daar volstaat `dieet | …`)
- geen ingredient-tags (dus niet `eiwit | linzen`)
- toegestane waarden staan in `tags_whitelist_facets.json` (`allowedByType.eiwit`)

Keuze van de juiste waarde:
- **kip** is alleen kip. Kalkoen krijgt `eiwit | kalkoen`, dus nooit `eiwit | kip` voor kalkoen.
- **wild** dekt zowel wildvogels (fazant, duif, kwartel) als wildvlees (hert, ree, everzwijn, haas).
  Let op: `haas` is het dier (wild), niet de varkenshaas of runderhaas; die vallen onder varken/rund.
- **gefokt gevogelte zonder eigen waarde** (eend, gans, parelhoen) heeft nog geen waarde: laat `eiwit`
  dan weg in plaats van een verkeerde waarde te kiezen.
- **vis** is vis; schaal- en weekdieren (garnaal, gamba, mossel, inktvis) krijgen `schaal-schelp`.
- **vleeswaren** (bacon, ham, chorizo) zijn meestal smaakmaker, geen hoofd-eiwitbron. Kies ze alleen als
  er geen ander dierlijk hoofdbestanddeel is.
- bij een mix zonder duidelijke hoofdbron (bijv. half-om-half gehakt) of bij onbepaald `gehakt`: laat
  `eiwit` weg.

## pittig (optioneel, exact 0 of 1 per recept)
Doel: filteren op “hoe spicy is dit?” zonder een algemene eigenschap-vergaarput.

Toegestane waarden:
- `pittig | mild`   (niet of nauwelijks pittig)
- `pittig | medium` (duidelijk pittig, maar voor de meeste mensen eetbaar)
- `pittig | heet`   (echt pittig; voor liefhebbers)

Regels:
- gebruik **max 1** pittig-tag per recept
- twijfel? laat weg (geen tag is ook een keuze)

### Hoe bepaal je pittig?
Gebruik een **pragmatische** inschatting voor een “gemiddelde NL-eter” en kijk naar:
- **Ingrediënten & hoeveelheid** (per ~4 porties):
  - *mild*: geen chili/peper, of alleen een klein beetje (bijv. 1 milde chili zonder zaadjes) of “optioneel naar smaak”
  - *medium*: 1–2 (milde/medium) chili’s of merkbaar chili-component (bijv. chilivlokken/poeder) zonder dat het als “heel heet” bekend staat
  - *heet*: meerdere chili’s, hete pepers (bijv. habanero/scotch bonnet), veel chilivlokken/poeder, of recept/bron noemt expliciet “very hot”/“spicy”
- **Tekstsignalen** in titel/omschrijving (woorden als “heet”, “pittig”, “spicy”, “hot”)
- **Serveertips** (bijv. waarschuwingen, “alleen voor liefhebbers”, extra koeling nodig)

Praktisch:
- Als je het gerecht makkelijk “niet pittig” kunt maken (chili geheel optioneel), tag dan meestal **niet** of kies **mild**.
- Als je je oude tag `pittig` moet mappen: gebruik standaard `pittig | medium`.


## Wat we NIET taggen
Niet toegestaan als tag:
- ingrediënten (aardappel, basilicum, linzen, etc.)
- bereidingsmethodes/apparatuur (oven, wok, pan, etc.)
- mood/subjectief (lekker, favoriet, “gezond-ish”)
- technische/irrelevante tags (bijv. `nextcloud`)
- samengestelde tags

## Tag-budget per recept
Streef naar **2–6 tags** totaal.

Richtlijnen per type:
- `tijd | …`: **exact 1** (verplicht)
- `keuken | …`: **0–1** (2 alleen bij fusion)
- `dieet | …`: **0–3**
- `eiwit | …`: **0–1** (alleen dierlijk; weglaten bij vegetarisch/vegan)
- `pittig | …`: **0–1**
