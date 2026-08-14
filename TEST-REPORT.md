# Vores Camping v31.0 – Test Report

Dato: 14. august 2026

## Resultat

**47/47 statiske integrationschecks bestået.**

Derudover er `app.js` og `sw.js` valideret med Node syntax-check, manifestet er valideret som JSON, og centrale filer/assets er serveret med HTTP 200 fra en lokal statisk server.

## Kontrolleret i v31.0

- Appversion er v31.0, mens eksisterende `voresCamping.v30.state` bevares.
- Routing, Geocoding, POI, Elevation og Optimization har hver sit konfigurerbare endpoint.
- Indstillinger indeholder felter til alle fem geotjenester.
- Testcenteret indeholder tests til OpenRouteService/Geocoding, OpenPOIService, OpenElevationService og VROOM.
- OpenPOIService opdeler `category_ids` i batches på højst fem.
- Standard OpenPOIService-buffer begrænses til 2 km.
- OpenElevationService `/point` og `/line` er koblet ind.
- Rutehøjde kan gemmes som samlet stigning/fald og min./maks. højde.
- Den aktive v31-ruteeditor indeholder **Optimer stop** til VROOM.
- VROOM-optimering bevarer start/slut og omarrangerer mellemstop.
- PWA service worker bruger nyt cache-navn `vores-camping-v31-0-shell`.
- Alle filer i service workerens lokale shell-cache findes.
- Nye logo-, app-ikon- og Ferie Vagt-assets findes i `/docs/assets`.
- PWA-ikonerne er 192×192 og 512×512.
- De fire valgfrie serverprojekter findes under `optional-services/source/`.
- ORS-referencepakken findes under `reference/openrouteservice/`.
- CSS-klammebalance er kontrolleret.

## Statisk serverkontrol

Følgende blev serveret med HTTP 200:

- `/`
- `/app.js`
- `/styles.css`
- `/manifest.webmanifest`
- `/sw.js`
- `/assets/app-icon.webp`
- `/assets/ferie-vagten/clipboard.webp`

## Browser-/runtime-test

Den tidligere v30.5-base havde et fuldt Chromium-regressionscheck. For v31.0 blev en ny headless Chromium-kørsel forsøgt, men den aktuelle sandbox blokerer administrativt både localhost- og `file://`-navigation med `ERR_BLOCKED_BY_ADMINISTRATOR`. Derfor påstår denne rapport ikke, at et komplet browser-regressionsflow er genkørt her.

Det indbyggede Testcenter i appen er udvidet, så de eksterne geotjenester kan testes direkte efter deploy på den enhed/browser, hvor appen skal bruges.

## Eksterne API'er

Live-kald til HeiGIT-standardtjenesterne er ikke gennemført uden brugerens ORS-nøgle. Selvhostede endpoints er heller ikke startet som del af GitHub Pages-pakken; de medfølgende projekter kræver deres egne data, konfiguration og servermiljø.
