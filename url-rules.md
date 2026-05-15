# URL input (receptpagina)

## Wanneer
Als de gebruiker een URL plakt (met of zonder foto's).

## Regels
- Als de pagina bereikbaar is: extraheer receptgegevens van de pagina (titel, ingrediënten, stappen, yield, tijden, cuisine/diet indien expliciet).
- Als de pagina niet bereikbaar of onduidelijk is: vraag om de recepttekst te plakken of een screenshot/foto te uploaden.
- Als de gebruiker een URL gaf: zet top-level `"url"` in de output op die URL (exacte string).
- Neem geen tracking/utm parameters over als je ze kunt herkennen en veilig verwijderen.
- Geen websearch buiten de gegeven URL in RECEPT-modus.

## URL basis
- Als de gebruiker een URL gaf: zet top-level `"url"` in de output op die URL (exacte string).
- Neem geen tracking/utm parameters over als je ze kunt herkennen en veilig verwijderen.
- Geen websearch buiten de gegeven URL in RECEPT-modus.

## Image (schema.org `image`) bij URL import
- Als de receptpagina een duidelijke hoofdafbeelding heeft: zet top-level `"image"` op de **absolute** image-URL.
- Bronvolgorde (eerste beschikbare):
  1) schema.org Recipe `image` op de pagina (als aanwezig)
  2) OpenGraph `og:image`
  3) Twitter Card `twitter:image`
  4) Duidelijke "hero" / hoofdafbeelding bij het recept (geen iconen/thumbnails)
- Gebruik geen data-URI's. Als alleen relatieve URL: maak absoluut met de site basis-URL.
- Als er meerdere goede afbeeldingen zijn: kies de eerste/hoofdafbeelding. (Geen array nodig.)
