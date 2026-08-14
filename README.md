# Vores Camping v31.0

Personlig camping-, ferie-, kort-, rute- og mindeapp som statisk PWA. v31.0 samler v30.5 med de nye logo-/Ferie Vagt-assets og gør geotjenesterne modulære, så appen både kan bruge HeiGIT-standardtjenester og egne HTTPS-endpoints.

## Udgivelse på GitHub Pages

1. Læg indholdet af denne pakke i repository-roden.
2. Sørg for at `docs/` ligger direkte i `main`.
3. GitHub → Settings → Pages.
4. Vælg **Deploy from a branch**.
5. Branch: **main**.
6. Folder: **/docs**.

Der kræves ingen npm-installation, intet build-trin og ingen GitHub Action. Kun `docs/` bliver publiceret af GitHub Pages.

## Data og opgradering

v31.0 bruger fortsat `voresCamping.v30.state`. Eksisterende v30.x-data kan derfor fortsætte ved opgradering på samme domæne/browserprofil.

OpenRouteService- og MapTiler-nøgler gemmes separat i browserens lokale lager og medtages ikke i den almindelige backup.

## Kort og geotjenester

- **MapLibre GL** er hovedmotor.
- **OpenFreeMap/OpenStreetMap** bruges som standardkort.
- **MapTiler** kan bruges til Satellite/Hybrid via egen nøgle.
- **OpenRouteService** bruges til routing og isochrones/rækkeviddekort.
- **Pelias/Geocoding** bruges til adresse- og stedsøgning.
- **OpenPOIService** bruges til interessepunkter omkring et sted.
- **OpenElevationService** kan supplere ruter og områder med højdedata.
- **VROOM** kan optimere rækkefølgen af mellemliggende rutestop.
- **Google Maps** er kun hjælpefunktion til links og delte ruter; det er ikke appens hovedkort.

Under **Indstillinger → Kort** kan hvert endpoint ændres. Standardværdierne peger på HeiGIT-tjenesterne og bruger ORS-nøglen, hvor det kræves. Et ændret endpoint behandles som selvhostet og kræver ikke automatisk ORS-nøglen.

## Medfølgende serverkilder

Mappen `optional-services/source/` indeholder de uploadede kilder til:

- OpenPOIService
- OpenElevationService
- VROOM Docker
- Pelias Docker

De kører **ikke inde i GitHub Pages**. De er med som valgfri backend-kilder, der kan sættes op på en separat server/VPS/NAS/Docker-host og derefter kobles til appen via HTTPS. Se `optional-services/README.md`.

Mappen `reference/openrouteservice/` indeholder den uploadede ORS-referencepakke, der er brugt til endpoint-, limit- og requesttilpasningerne i v31.0.

## v31.0 højdepunkter

- Nyt Vores Camping-logo, app-ikon og opdaterede PWA-ikoner.
- Nye Ferie Vagt-figurer og separate Ferie Vagt-props som app-assets.
- Konfigurerbare endpoints til Routing, Geocoding, POI, Elevation og VROOM.
- OpenPOIService-søgning opdeles automatisk i små kategori-batches og standardtjenesten begrænses til 2 km pr. POI-kald.
- OpenElevationService supplerer ruteprofilen, hvis rutetjenesten ikke allerede returnerer højdekoordinater.
- Ruter kan vise samlet stigning og højeste punkt.
- VROOM-knappen **Optimer stop** kan omarrangere mellemliggende stop og bevare start/slut.
- Udvidet Testcenter med separate forbindelsestests til ORS/geocoding, OpenPOIService, OpenElevationService og VROOM.
- GitHub Pages-strukturen er bevaret: hele den publicerbare app ligger fortsat i `/docs`.

## Vigtigt om egne tjenester

Når appen kører fra GitHub Pages, skal egne server-endpoints kunne kaldes fra browseren. De bør derfor være tilgængelige via **HTTPS** og have **CORS** konfigureret til din GitHub Pages-adresse. Pelias, OpenPOIService, OpenElevationService og VROOM kræver desuden hver deres data-/backendopsætning; kildekoden alene gør dem ikke til en færdig hosted API.
