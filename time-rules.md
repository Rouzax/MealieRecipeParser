# Tijden (schema.org Recipe): bron gaat voor, anders conservatief bepalen

## Velden (top-level)
- prepTime, cookTime, totalTime, performTime: ISO 8601 durations (bv. PT20M, PT1H10M).

## Normaliseren
- "70 min" -> PT1H10M
- "1:10" -> PT1H10M
- "1 uur 10 minuten" -> PT1H10M
- Ranges "45–60 min": voor duurvelden gebruik ondergrens PT45M; behoud de range in staptekst.

## Bron gaat voor (BELANGRIJK)
Als het bronrecept expliciet een **totaaltijd** en/of **prep/cook** tijden geeft (bv. in metadata of kopje “tijd”):
- Neem die waarden over (genormaliseerd naar ISO 8601).
- Ga NIET opnieuw optellen uit de stappen “omdat het anders uitkomt”.

Prioriteit:
1) Expliciet opgegeven tijdvelden uit de bron (total/prep/cook/perform)
2) Anders: conservatief optellen uit expliciete tijden in tekst/stappen (zie hieronder)
3) Anders: tijdveld weglaten

## Optellen (alleen als bron géén tijdveld geeft)
Je mag tijden optellen alleen als:
- elke tijd expliciet genoemd is,
- tijden sequentieel zijn en niet overlappen,
- je duidelijk kunt indelen of het prep of cook is.

Aanbevolen:
- prepTime = som van expliciete voorbereidingstijden (snijden, wassen, weken, marineren, rusten) die vóór koken/bakken plaatsvinden.
- cookTime = som van expliciete kook/baktijden.
- performTime = alleen als expliciet genoemd of heel duidelijk af te grenzen; anders weglaten.
- totalTime = alleen als je alle componenten expliciet en niet-overlappend hebt; anders weglaten.
