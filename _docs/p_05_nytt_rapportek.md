---
layout: page
title: "Hvordan lage en ny Rapporteket-applikasjon"
---

Beskrivelsen under er ikke nødvendigvis utfyllende og forutsetter kjennskap til R og bruk av git og GitHub.
Som en ekstra støtte anbefales [R pacakges](http://r-pkgs.had.co.nz/) av Hadley Wickham og spesielt [beskrivelsen av git og GitHub](http://r-pkgs.had.co.nz/git.html#git-rstudio).

## Lag ditt eget prosjekt basert på templatet

Denne delen kan være relevant om det er ønskelig å benytte templatetet som utgangspunkt for etablering av nye registre på Rapporteket.

1. Hent ned prosjektet [rapRegTemplate](https://github.com/Rapporteket/rapRegTemplate)
```bash
git clone https://github.com/Rapporteket/rapRegTemplate.git appnavn
```
2. Slett mappen `.git`
3. Initiér nytt *git repository*
```bash
  git init .
  git add .
  git commit -m "init commit"
  ```
4. Erstatt `rapRegTemplate` med valgfritt pakkenavn i koden og rydd i prosjektet (f.eks. ved bruk av *vscode*). Husk å *commit* underveis.
5. Bygg, installér og kjør pakken i R/RStudio. Test gjerne at innebygget Shiny-applikasjon fungerer på samme vis som i prosjektet "rapRegTemplate"

## Opprett database for logging og abonnement

Mye av kjernefunksjonaliteten i Rapporteket og [*rapbase*](https://github.com/Rapporteket/rapbase) er avhengig av at det finnes databaser for logging og abonnement. Kode for å lage disse ligger i pakken *rapbase* og gjengis her.

### Abonnement-database

Miljøvariablen `MYSQL_DB_AUTOREPORT` brukes av *rapbase* for å finne navnet på abonnement-databasen. Hvis man har abonnement-funksjonalitet i sitt rapportek, må denne miljøvariabelen defineres:
```r
Sys.setenv(MYSQL_DB_AUTOREPORT="db_autoreport")
```
Navnet `db_autoreport` er valgfritt.

Selve databasen lages slik:

```sql
CREATE DATABASE IF NOT EXISTS `db_autoreport`
USE `db_autoreport`;

CREATE TABLE IF NOT EXISTS `autoreport` (
  `id` varchar(255) COLLATE utf8mb4_danish_ci DEFAULT NULL,
  `synopsis` varchar(255) COLLATE utf8mb4_danish_ci DEFAULT NULL,
  `package` varchar(255) COLLATE utf8mb4_danish_ci DEFAULT NULL,
  `fun` varchar(255) COLLATE utf8mb4_danish_ci DEFAULT NULL,
  `params` text COLLATE utf8mb4_danish_ci,
  `owner` varchar(255) COLLATE utf8mb4_danish_ci DEFAULT NULL,
  `email` varchar(255) COLLATE utf8mb4_danish_ci DEFAULT NULL,
  `organization` varchar(255) COLLATE utf8mb4_danish_ci DEFAULT NULL,
  `terminateDate` varchar(255) COLLATE utf8mb4_danish_ci DEFAULT NULL,
  `interval` varchar(255) COLLATE utf8mb4_danish_ci DEFAULT NULL,
  `intervalName` varchar(255) COLLATE utf8mb4_danish_ci DEFAULT NULL,
  `runDayOfYear` text COLLATE utf8mb4_danish_ci,
  `type` varchar(255) COLLATE utf8mb4_danish_ci DEFAULT NULL,
  `ownerName` varchar(255) COLLATE utf8mb4_danish_ci DEFAULT NULL,
  `startDate` varchar(255) COLLATE utf8mb4_danish_ci DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_danish_ci;
```

### Logg-database

Når rapporteket-applikasjonen starter opp og brukes, skrives det til to tabeller i en logg-database. Dette kommer i tillegg til det som logges i Norsk Helsenett sine systemer. Det skriver til disse to tabellene når *rapbase*-funksjonene `appLogger`, `repLogger` og `autLogger` brukes. Se [rapbase sin dokumentasjon](https://rapporteket.github.io/rapbase/reference/logger.html) for mer informasjon om bruk av disse funksjonene.

Miljøvariablen `MYSQL_DB_LOG` brukes av *rapbase* for å finne navnet på logg-databasen, og må defineres:
```r
Sys.setenv(MYSQL_DB_LOG="db_log")
```
Navnet `db_log` er valgfritt.

Selve databasen lages slik:
```sql
CREATE DATABASE IF NOT EXISTS `db_log`;
USE `db_log`;

CREATE TABLE IF NOT EXISTS `appLog` (
  `id` int(9) unsigned NOT NULL AUTO_INCREMENT,
  `time` datetime DEFAULT NULL,
  `user` varchar(127) COLLATE utf8_danish_ci DEFAULT NULL,
  `name` varchar(255) COLLATE utf8_danish_ci DEFAULT NULL,
  `group` varchar(63) COLLATE utf8_danish_ci DEFAULT NULL,
  `role` varchar(63) COLLATE utf8_danish_ci DEFAULT NULL,
  `resh_id` varchar(31) COLLATE utf8_danish_ci DEFAULT NULL,
  `message` varchar(2047) COLLATE utf8_danish_ci DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_danish_ci;


CREATE TABLE IF NOT EXISTS `reportLog` (
  `id` int(9) unsigned NOT NULL AUTO_INCREMENT,
  `time` datetime DEFAULT NULL,
  `user` varchar(127) COLLATE utf8_danish_ci DEFAULT NULL,
  `name` varchar(255) COLLATE utf8_danish_ci DEFAULT NULL,
  `group` varchar(63) COLLATE utf8_danish_ci DEFAULT NULL,
  `role` varchar(63) COLLATE utf8_danish_ci DEFAULT NULL,
  `resh_id` varchar(31) COLLATE utf8_danish_ci DEFAULT NULL,
  `environment` varchar(63) COLLATE utf8_danish_ci DEFAULT NULL,
  `call` varchar(2047) COLLATE utf8_danish_ci DEFAULT NULL,
  `message` varchar(2047) COLLATE utf8_danish_ci DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_danish_ci;
```




