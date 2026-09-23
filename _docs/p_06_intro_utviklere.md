---
layout: page
title: "For utviklere av Rapporteket"
nav_order: 6
---

Rapporteket er en Shiny-app utviklet i R.
Dette betyr at det meste av funksjonaliteter som trengs for å utvikle applikasjonene er generelle funksjoner som er tilgjengelige i R-universet.
Det er likevel noen spesielle ting som gjør Shiny-applikasjonen til en Rapporteket-applikasjon.
Dette er:

-	**rapbase-funksjoner:** Rapbase er en pakke som tilbyr en rekke spesialiserte Rapporteket-funksjoner. Det er Nasjonalt Servicemiljø som vedlikeholder denne pakken, men vi ønsker velkomne forslag og tillegg her. Vi jobber med å dokumentere funksjonene så godt det lar seg gjøre. De essensielle funksjonene som må brukes er:
    - `navbarWidgetServer2`/`navbarWidgetInput` for å hente ut brukernavn, rolle og tilhørighet som kommer fra FALK.
    - `repLogger`/`appLogger` for å logge til Rapporteket sine logg-databaser.
    - `loadRegData` for å kjøre spørringer mot database.
    - `autoReportServer`/`autoReportInput`/`autoReportUI` for å sette opp autorapport-utsending.
    - `loggerSetup` for å få ut logg i `json`-format.
 
-	**Miljøvariabler:** På Norsk Helsenett lagres informasjon om brukeren og Rapporteket kan tilpasses denne brukeren slik at data blir tilgjengelig basert på brukerens tilhørighet eller rolle i registeret. I tillegg er det viktig å logge hvem som ser dataene. For å kjøre applikasjonen lokalt må nødvendige miljøvariabler defineres. Dette kan enten defineres i `.Renviron`, i `.Rprofile` ved hjelp av `Sys.setenv()`, i `docker-compose.yml`-fil eller i egen R-fil som *sources* før kjøring av applikasjon. Miljøvariabler som er essensielle er:
    - `FALK_EXTENDED_USER_RIGHTS`
    - `FALK_APP_ID`
    - `MYSQL_DB_LOG`
    - `MYSQL_DB_AUTOREPORT`
    - `MYSQL_DB_DATA`
    - `MYSQL_HOST`
    - `MYSQL_USER`
    - `MYSQL_PASSWORD`
    - `USERORGID`
    - `SHINYPROXY_USERNAME`
    - `SHINYPROXY_USERGROUPS`
    - `SHINYPROXY_APPID`
    - `R_RAP_INSTANCE`
    - `R_RAP_CONFIG_PATH`

-	**Docker Container:** Applikasjonen skal kjøres i en Docker Container på Norsk Helsenett. Ved publisering av ny versjon av en Rapporteket-applikasjon bygges et *image* på github gjennom en github-action. Dette image dyttes så opp til NHN. For utviklere som har slik software tilgjengelig kan det være lurt å kjøre applikasjonen lokalt også i en container for å få testet applikasjonen i et så likt miljø som mulig.
-	**Databaser:** Rapporteket-applikasjonen er avhengig av at det finnes databaser for logging og abonnement. Kode for å lage disse ligger i pakken *rapbase* og må kjøres mot en databaseserver som utvikleren har tilgang til. I tillegg skal applikasjonen ha tilgang til database som inneholder registerdata. Det finnes funksjonalitet i *rapbase* for å hente ned databasedump fra NHN for å kunne teste lokalt.
-	**R-pakke:** Erfaring tilsier at det er enklest og best å utvikle applikasjonen som en R-pakke. Dette er fordi det gir god struktur på koden og gjør det enklere å vedlikeholde applikasjonen over tid. Det vil si at utvikleren utvikler applikasjonen etter retningslinjene for pakke-bygging i R.

## Dette trenger du for å utvikle Rapportek:

For å kunne utvikle Rapportek-applikasjon trenger man

- R og RStudio installert
- kjennskap til R og Shiny
- Git installert
- et *repository* på  [github.com/Rapporteket](https://github.com/Rapporteket/) (dette lages av SKDE)
- kjennskap til git og GitHub
- databaseinnstallasjon (MySQL/MariaDB)
- LaTeX installert

I tillegg er det nyttig med docker installert for å kunne teste applikasjonen i et så likt miljø som mulig som det den skal kjøres på NHN.
