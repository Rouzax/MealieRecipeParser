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

## eiwit (optioneel, max 2 per recept; alleen dierlijk)
Doel: filteren op belangrijke dierlijke eiwitbronnen bij niet-vegetarische recepten.

Regels:
- tag elke **duidelijke dierlijke hoofdcomponent**
- bij twee gelijkwaardige hoofdbronnen: tag beide
- bij **meer dan twee** bronnen: kies de twee dominante, of laat `eiwit` weg als er geen twee
  duidelijk uitspringen
- een **keuze** tussen twee soorten ("runder- of lamsgehakt") is geen mix: dat is een variant,
  geen tweede bron. Tag de eerstgenoemde, of laat weg als het recept geen voorkeur uitspreekt
- een kleine hoeveelheid als smaakmaker (bijv. bacon, ham, chorizo) telt niet mee naast een
  andere hoofdbron
- niet gebruiken bij vegetarisch/vegan (daar volstaat `dieet | …`)
- geen ingredient-tags (dus niet `eiwit | linzen`)
- bij onbepaald vlees of `gehakt` zonder genoemde diersoort: laat `eiwit` weg
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

Voorbeelden:
- 500 g rundergehakt -> `eiwit | rund`
- 500 g half-om-half gehakt -> `eiwit | rund` + `eiwit | varken`
- 250 g rund + 250 g varken -> `eiwit | rund` + `eiwit | varken`
- 500 g kip + 75 g bacon -> `eiwit | kip`
- 500 g runder- of lamsgehakt -> `eiwit | rund`
- 200 g gehakt, soort niet genoemd -> geen `eiwit`
- 400 g eendenborst -> geen `eiwit` (nog geen toegestane waarde)
- kip, chorizo en garnalen in een gerecht -> kies de twee dominante, of laat weg

## pittig (optioneel, exact 0 of 1 per recept)
Doel: filteren op “hoe spicy is dit?”.

`pittig` meet de ervaren scherpte of hitte van het uiteindelijke gerecht voor een gemiddelde
Nederlandse eter. Het meet **niet** hoe sterk of aromatisch een gerecht gekruid is.

Toegestane waarden:
- `pittig | mild`   (geen of nauwelijks waarneembare hitte)
- `pittig | medium` (duidelijke maar goed eetbare hitte)
- `pittig | heet`   (uitgesproken of dominante hitte)

Regels:
- gebruik **max 1** pittig-tag per recept
- twijfel? laat weg (geen tag is ook een keuze)
- beoordeel indien mogelijk relatief aan ongeveer 4 porties
- expliciete uitspraken van de bron over **hitte** wegen zwaar; “spiced” of “well-spiced” betekent
  niet automatisch pittig

### Hoe bepaal je pittig?
Beoordeel eerst expliciete uitspraken van de bron, kijk daarna naar soort, hoeveelheid en
bereidingswijze van scherpe ingrediënten:
- **Chili** telt altijd mee. Houd rekening met het type: Kashmiri-chili is relatief mild;
  habanero, scotch bonnet en bird’s eye zijn heet.
- **Zwarte/witte peper** telt alleen duidelijk mee als het een dragende component is, niet als
  gewone kruiderij.
- **Mosterd, mierikswortel, wasabi en verse gember** kunnen meetellen als hun scherpte duidelijk
  aanwezig blijft, vooral rauw of kort verhit.
- Langdurig verhitte mosterdolie of meegestoofde gember telt normaal niet zelfstandig mee.

Aromatische specerijen zoals kardemom, kruidnagel, kaneel/cassia, komijn, korianderzaad, kurkuma,
venkel, foelie en garam masala tellen **niet** mee voor pittigheid.

### Ankers per ~4 porties
- *mild*: geen chili, slechts een kleine hoeveelheid milde chili, of chili die optioneel is dan wel
  apart wordt geserveerd
- *medium*: 1–2 milde/medium chili’s of een duidelijk merkbare chili-component
- *heet*: meerdere chili’s, hete chilisoorten (habanero, scotch bonnet, bird’s eye), veel
  chilipoeder of -vlokken, of door de bron expliciet als heet beschreven

Praktisch:
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
- `eiwit | …`: **0–2** (alleen dierlijk; weglaten bij vegetarisch/vegan; 2 alleen bij een
  echte mix, zoals half-om-half gehakt)
- `pittig | …`: **0–1**
