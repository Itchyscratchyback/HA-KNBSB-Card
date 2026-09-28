# Aanbevolen dashboardlayout

Voor de beste weergave wordt een Home Assistant **Masonry View** aanbevolen.

Gebruik bijvoorbeeld:

```yaml
views:
  - title: KNBSB
    path: knbsb
    type: masonry
    cards:
      - type: custom:knbsb-schedule-card
        entity: sensor.knbsb_schedule

```

KNBSB Schedule Card voor Home Assistant
Een custom dashboardkaart voor de KNBSB-integratie voor Home Assistant.

De KNBSB Schedule Card toont het volledige wedstrijdprogramma van een KNBSB-team als overzichtelijke wedstrijdkaarten.

Deze kaart is bedoeld als frontend voor de aparte KNBSB Home Assistant-integratie.

Functionaliteit
De KNBSB Schedule Card toont automatisch alle wedstrijden uit:

sensor.knbsb_schedule
Iedere wedstrijd wordt als een afzonderlijke kaart weergegeven.

De kaart toont onder andere:

Thuisteam
Uitteam
Teamlogo's
Wedstrijddatum
Wedstrijdtijd
Thuis / Uit voor het gevolgde team
Wedstrijdlocatie
Adres
Competitie
Rijafstand
Reistijd
Geplande aankomsttijd
Vertrektijd vanaf huis
Navigatie via Google Maps
De eerstvolgende wedstrijd wordt automatisch gemarkeerd als:

VOLGENDE WEDSTRIJD
Voorbeeld
Een wedstrijdkaart bevat bijvoorbeeld:
https://github.com/Itchyscratchyback/HA-KNBSB-Schedule-card/blob/main/images/screenshot-1.png
https://github.com/Itchyscratchyback/HA-KNBSB-Schedule-card/blob/main/images/screenshot-2.png


Vereisten
De KNBSB Schedule Card heeft de KNBSB backend-integratie nodig.

Backend repository:

https://github.com/Itchyscratchyback/HA-KNBSB
De backend moet minimaal deze entity leveren:

sensor.knbsb_schedule
De kaart haalt alle benodigde wedstrijdinformatie uit het attribuut:

matches
Installatie via HACS
Stap 1
Installeer eerst de KNBSB backend-integratie:

https://github.com/Itchyscratchyback/HA-KNBSB
Configureer daarna een KNBSB-team in Home Assistant.

Controleer of deze entity bestaat:

sensor.knbsb_schedule
Stap 2
Open HACS.

Ga naar:

HACS
→ Frontend
→ Custom repositories
Voeg de repository van de KNBSB Schedule Card toe.

https://github.com/Itchyscratchyback/HA-KNBSB-Card
Selecteer als repositorytype:

Dashboard
of het frontend/plugin-type dat door de gebruikte HACS-versie wordt aangeboden.

Stap 3
Installeer:

KNBSB Schedule Card
Na installatie kan een herstart of harde browser-refresh nodig zijn.

Dashboard gebruiken
Voeg de kaart toe aan een Home Assistant dashboard.

Gebruik:

type: custom:knbsb-schedule-card
entity: sensor.knbsb_schedule
Dat is de volledige minimale configuratie.

De kaart haalt daarna automatisch alle beschikbare wedstrijden op.

Volledig dashboardvoorbeeld
views:
  - title: KNBSB
    path: knbsb
    icon: mdi:baseball
    cards:
      - type: custom:knbsb-schedule-card
        entity: sensor.knbsb_schedule
Responsive weergave
De kaart past zich automatisch aan de beschikbare schermbreedte aan.

Op een klein scherm worden wedstrijden onder elkaar weergegeven.

[ Wedstrijd 1 ]

[ Wedstrijd 2 ]

[ Wedstrijd 3 ]
Wanneer voldoende ruimte beschikbaar is kunnen meerdere wedstrijden naast elkaar worden weergegeven.

[ Wedstrijd 1 ]  [ Wedstrijd 2 ]

[ Wedstrijd 3 ]  [ Wedstrijd 4 ]
Op brede dashboards kunnen nog meer kaarten naast elkaar passen.

De minimale breedte van een wedstrijdkaart voorkomt dat teamnamen, logo's en wedstrijdinformatie te smal worden weergegeven.

Thuisteam en uitteam
De kaart gebruikt altijd dezelfde wedstrijdvolgorde:

THUISTEAM VS UITTEAM
Het thuisteam staat altijd links.

Het uitteam staat altijd rechts.

Voorbeeld:

THUIS                         UIT

UVV             VS     Houten Dragons
Bij een thuiswedstrijd van het gevolgde team:

THUIS                         UIT

Houten Dragons   VS          Red Caps
Deze volgorde staat los van het team dat in de KNBSB backend wordt gevolgd.

Gevolgd team
De kaart toont daarnaast of het in de backend ingestelde team thuis of uit speelt.

Voorbeeld:

Gevolgd team: Uit
of:

Gevolgd team: Thuis
Teamlogo's
De logo's van het thuis- en uitteam worden automatisch via de KNBSB backend aangeleverd.

De kaart gebruikt:

home_team_logo
en:

away_team_logo
uit het wedstrijdobject.

Wanneer geen logo beschikbaar is kan de kaart een eenvoudige fallback tonen.

Eerstvolgende wedstrijd
De eerste wedstrijd in het programma wordt automatisch gemarkeerd.

Deze wedstrijd krijgt:

VOLGENDE WEDSTRIJD
en een visueel accent.

De backend levert het programma chronologisch aan.

Locatie
Per wedstrijd toont de kaart:

location
en:

address
Bijvoorbeeld:

Sportpark De Paperclip
Parkzichtlaan 201, 3451 GX Vleuten
Reisinformatie
Wanneer OpenRouteService in de backend correct is ingesteld, toont iedere wedstrijdkaart:

Rijafstand
Reistijd
Geplande aankomsttijd
Vertrektijd
Bijvoorbeeld:

38.2 km

32 minuten

Geplande aankomst
09:25

Vertrek vanaf huis
08:43
De berekeningen zelf worden niet door de dashboardkaart uitgevoerd.

Alle route- en planningsinformatie wordt door de KNBSB backend berekend.

Navigatie
Iedere wedstrijdkaart kan een knop tonen:

📍 Navigeer
De bestemming wordt bepaald aan de hand van:

latitude
longitude
uit de wedstrijdgegevens.

De knop opent Google Maps met de wedstrijdlocatie als bestemming.

Hierdoor kan iedere wedstrijd afzonderlijk als navigatiebestemming worden geopend.

Benodigde backendvelden
De frontend verwacht per wedstrijd minimaal de volgende structuur:

match_id:

date:
time:

home_team_name:
home_team_logo:

away_team_name:
away_team_logo:

home_away:
competition:

location:
address:

latitude:
longitude:

drive_distance:
drive_time:

arrival_time:
departure_time:
Deze structuur wordt geleverd door de KNBSB backend-integratie.

Backend en Card
De KNBSB-oplossing bestaat bewust uit twee afzonderlijke HACS-projecten.

Backend
HA-KNBSB
Verantwoordelijk voor:

KNBSB/Foys communicatie
OpenRouteService
Wedstrijdprogramma
Routeberekeningen
Vertrektijden
Aankomsttijden
Persistente route-cache
Home Assistant sensors
Home Assistant calendar
Repository:

https://github.com/Itchyscratchyback/HA-KNBSB
Frontend
HA-KNBSB-Card
Verantwoordelijk voor:

Visuele wedstrijdkaarten
Responsive layout
Teamlogo's
Volgende-wedstrijdmarkering
Reisinformatie tonen
Navigatieknop
De backend kan zonder de Schedule Card worden gebruikt.

De Schedule Card heeft de backend wel nodig.

Problemen oplossen
Custom element doesn't exist
Wanneer Home Assistant meldt:

Custom element doesn't exist:
knbsb-schedule-card
controleer eerst of de kaart via HACS geïnstalleerd is.

Voer daarna een harde browser-refresh uit.

Bijvoorbeeld:

Ctrl + F5
Op mobiele apparaten kan het nodig zijn de Home Assistant-app volledig af te sluiten en opnieuw te openen.

Oude kaart blijft zichtbaar
Browsers kunnen JavaScript-bestanden agressief cachen.

Na een update van de KNBSB Schedule Card:

Vernieuw Home Assistant.
Voer een harde browser-refresh uit.
Sluit indien nodig de Home Assistant-app volledig af.
Open de app opnieuw.
Geen wedstrijden zichtbaar
Controleer in:

Ontwikkelaarshulpmiddelen
→ Statussen
of deze entity bestaat:

sensor.knbsb_schedule
Controleer vervolgens het attribuut:

matches
Wanneer matches leeg is, ligt het probleem waarschijnlijk in de backend-configuratie of het KNBSB-programma en niet in de dashboardkaart.

Geen logo's zichtbaar
Controleer in:

sensor.knbsb_schedule
of iedere wedstrijd deze waarden bevat:

home_team_logo
away_team_logo
De waarden moeten geldige afbeelding-URL's bevatten.

Geen reisinformatie zichtbaar
Controleer of een wedstrijd in:

sensor.knbsb_schedule
waarden bevat voor:

drive_distance
drive_time
arrival_time
departure_time
Wanneer deze waarden ontbreken, controleer dan de OpenRouteService-configuratie van de KNBSB backend.

Navigatieknop ontbreekt
De navigatieknop wordt alleen weergegeven wanneer de wedstrijd geldige waarden bevat voor:

latitude
longitude
Controleer deze gegevens in:

sensor.knbsb_schedule
Beta-status
Huidige versie:

0.1.0-beta.1
Dit is de eerste beta-release van de KNBSB Schedule Card.

De kaart is ontwikkeld in combinatie met:

HA-KNBSB v0.1.0-beta.1
Tijdens de beta kunnen layout, functionaliteit en het wedstrijdobject verder worden uitgebreid.

Bestaande velden van het sensor.knbsb_schedule wedstrijdobject worden waar mogelijk compatibel gehouden.

Geplande functionaliteit
Mogelijke toekomstige uitbreidingen:

Uitslagen
Afgelopen wedstrijden
Wedstrijdstatus
Competitiestand
Extra wedstrijdstatistieken
Uitklapbare wedstrijddetails
Aanpasbare kleuren
Aanpasbare kaartgrootte
Configureerbare navigatieprovider
Problemen melden
Problemen kunnen via GitHub Issues worden gemeld.

Repository:

https://github.com/Itchyscratchyback/HA-KNBSB-Card
Vermeld bij een probleem indien mogelijk:

Home Assistant-versie
KNBSB backend-versie
KNBSB Schedule Card-versie
Of sensor.knbsb_schedule correcte gegevens bevat
Relevante foutmelding uit de browserconsole
Voeg geen OpenRouteService API-sleutel toe aan foutmeldingen of screenshots.

Disclaimer
Dit is een onofficieel communityproject.

KNBSB, clubnamen, clublogo's en competitiegegevens kunnen eigendom zijn van hun respectieve rechthebbenden.

De KNBSB Schedule Card is niet verbonden aan of goedgekeurd door KNBSB, Foys, Google Maps, OpenRouteService of HeiGIT.
