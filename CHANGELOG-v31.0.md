# Vores Camping v31.0 – ændringer

Dato: 14. august 2026

## Samlet app

- v30.5 er bevaret som frontend-base og opgraderet til v31.0.
- Eksisterende browserdata bevares via samme `voresCamping.v30.state`-lager.
- GitHub Pages-udgivelsen er fortsat ren statisk PWA fra `/docs`.

## Design og assets

- Udskiftet app-ikon og logo med de nye uploadede Vores Camping-designs.
- Genereret PWA-ikoner i 192×192 og 512×512.
- Udskiftet Ferie Vagten-figurer med de nye uploadede kattefigurer.
- Tilføjet separate ekstra Ferie Vagt-assets: skål, liggestol, skilte, walkie-talkie, skammel, drink, kuffert og hængekøje.

## Kort og geotjenester

- Tilføjet fælles servicekonfiguration for:
  - OpenRouteService routing/isochrones.
  - Pelias/geocoding.
  - OpenPOIService.
  - OpenElevationService.
  - VROOM optimization.
- Standard-endpoints peger på de relevante HeiGIT-tjenester.
- Egne endpoints kan indsættes under Indstillinger → Kort.
- ORS API-nøglen sendes kun automatisk til standard-HeiGIT-endpoints.
- Reverse geocoding, autocomplete, søgning og isochrones understøtter nu egne endpoints.

## OpenPOIService

- POI-kategorier er tilpasset den medfølgende ORS-referencepakke.
- `category_ids` opdeles i batches på højst fem pr. request.
- Standard OpenPOIService-kald begrænses til 2 km point-buffer; appens lokale gemte steder kan stadig filtreres med større radius.
- Egne POI-endpoints kan bruges til større/andre servicegrænser.

## OpenElevationService

- Højde kan vises for centrum på “Området omkring”.
- Ruter bruger først højdekoordinater fra routing-resultatet.
- Hvis disse mangler, kan OpenElevationService supplere ruten via `/line`.
- Rutehøjden samples til højst ca. 1900 koordinater før ekstern elevation-request.
- Gemte ruter kan indeholde samlet stigning, fald, minimum og maksimum højde.

## VROOM

- Tilføjet **Optimer stop** på den aktive ruteeditor.
- Start og destination fastholdes, mens mellemliggende stop sendes som jobs til VROOM.
- Ruteoptimering kan slås til/fra under Indstillinger.
- Maksimum 50 rutepunkter i appens VROOM-flow.

## Testcenter

- Tilføjet separate tests for OpenPOIService, OpenElevationService og VROOM.
- ORS/geocoding-testen accepterer nu enten ORS-nøgle eller eget endpoint.
- Komplet korttest bruger den aktive servicekonfiguration.

## Medfølgende backend-kilder

- OpenPOIService, OpenElevationService, VROOM Docker og Pelias Docker er placeret under `optional-services/source/`.
- Disse mapper ligger uden for `/docs` og publiceres derfor ikke som en del af GitHub Pages-appen.
