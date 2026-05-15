# Ingredientregels (recipeIngredient): Mealie Notes + DB-match met BLOKHAAKJES []

Schema.org `recipeIngredient` is een lijst strings. Mealie probeert hieruit kern + Notes te parsen.
Doel: consistente parsing én betere match met je Mealie ingrediënten-database.

## 1) Basisformat (Mealie Notes-truc)
Schrijf elke regel bij voorkeur als:
- **Kern vóór de eerste komma:** `<hoeveelheid> <eenheid> <ingrediëntnaam>`
- **Alles NA de eerste komma:** notities (snijwijze, duur, “naar smaak”, etc.)
- **Ronde haakjes `(...)`:** notes/extra context/alternatieven/aliases/buitenlandse naam
- **BLOKHAAKJES `[...]`:** DB-kwalificaties die onderdeel moeten blijven van de ingrediëntnaam (zie §2)

Richtlijn:
- 1 kern-ingrediënt vóór de komma.
- Alternatieven/aliases/buitenlandse namen in `(...)`.
- **Verwijder pagina-/boekverwijzingen volledig** (bv. “zie pag. 14”, “p. 14”, “pagina 14”). Niet bewaren.

## 2) BLOKHAAKJES `[...]` voor DB-kwalificaties (belangrijk)
Omdat `(...)` vaak als Notes geïnterpreteerd wordt, gebruik je `[...]` voor kwalificaties die juist
onderdeel moeten blijven van de ingrediëntnaam om DB-entries consistent te matchen.

Gebruik `[...]` voor vaste varianten zoals:
- maalvorm/vorm: `[gemalen]`, `[korrels]`, `[heel]`, `[vlokken]`, `[stokje]`, `[blad]`, `[zaad]`
- toestand: `[vers]`, `[gedroogd]`
- afgeleide vorm: `[sap]`, `[rasp]`, `[schil]` (alleen als je DB dit zo heeft)

Voorbeelden:
- `zwarte peper [korrels]`
- `zwarte peper [gemalen], naar smaak`
- `koriander [blad], grof gehakt` (als je DB dit zo heeft)

## 3) Buitenlandse ingrediëntnamen -> NL kern (omdraaien)
Als een ingrediëntregel de vorm heeft: `<buitenlandse naam> (<Nederlandse uitleg/naam>)`
en de Nederlandse naam is gangbaar:
- **Draai om** naar: `<Nederlandse naam> (<buitenlandse naam>)`

Voorbeeld:
- `masoor dal (rode splitlinzen)` → `rode splitlinzen (masoor dal)`

Als er géén gangbare NL naam bekend/afleidbaar is:
- behoud de originele kern (niet gokken).

## 4) Poeder-uitzondering
Als “Xpoeder” de gangbare productnaam is (en/of zo in de bron staat), gebruik die als kern:
- `knoflookpoeder`, `uienpoeder`, `gemberpoeder`, `kaneelpoeder`, `paprikapoeder`, `chilipoeder`

## 5) Voorbeelden (goed)
- `1/2 ui, fijngesneden`
- `5 teentjes knoflook, in plakjes`
- `300 g rode splitlinzen (masoor dal), afgespoeld`
- `1 el koolzaadolie (of kruidolie), om te bakken`
- `1 tl fenegriekblad [gedroogd] (methi)`
- `zwarte peper [gemalen], naar smaak`

## 6) Vervangingen (moeilijk verkrijgbare ingrediënten)
Soms geeft de bron een alternatief als een ingrediënt lastig te krijgen is (bv. “als shatkora niet beschikbaar is, gebruik grapefruit…”).

Regel:
- Leg de vervanging vast in de **zelfde ingredientregel** in ronde haakjes met een duidelijke prefix:
  - `(vervanging: …)`
- Houd de kern als het originele ingrediënt (zodat je nog weet wat “echt” bedoeld was).
- Voeg ook de vervangende hoeveelheid toe als die expliciet genoemd is.

Voorbeeld (uit bron-notes):
- `1 shatkora (vervanging: 1/2 grapefruit, sap en schil)`
- `1 tl gedroogd fenegriekblad (methi) (vervanging: 1 tl fenegriekzaad)`

Optioneel (alleen als het verduidelijking nodig heeft):
- Voeg één extra HowToStep toe aan het begin of bij de eerste keer dat het ingrediënt gebruikt wordt:
  - “Geen shatkora? Gebruik sap en schil van 1/2 grapefruit.”
