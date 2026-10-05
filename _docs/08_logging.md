---
layout: page
title: "Hva og hvordan logger vi"
nav_order: 8
permalink: /logging
---

## Når logges det?

Følgende hendelser logges automatisk for alle Rapporteket‑applikasjoner som benytter rapbase versjon 3.7.0 eller nyere, både til logg-databasen og NHNs interne loggsystemer:
- Oppstart av applikasjon.
- Når bruker endrer rolle eller enhet i applikasjonen.
- Når bruker laster ned en databasedump eller en tabell via rapbase‑funksjoner.
- Ved automatisk utsending av e‑poster: hvilken rapport som er sendt og hvilke mottakere som fikk den.

Utviklere av Rapporteket‑applikasjoner legge inn ekstra logging der det er nødvendig.

## Hva logges?

For alle logghendelser registreres følgende informasjon:
- Tidspunkt
- Navn på applikasjon
- Navn på bruker
- Epost-adresse
- Brukerrolle
- Enhet (ReshID)

## Hvordan legger man inn ekstra logging?

Ved å bruke funksjonen `repLogger` fra pakken `rapbase` logges beskjeder til logg-databasen:
```R
rapbase::repLogger(msg = "Tekst som logges")
```

Hvis man er i et interaktivt miljø og har tilgang til `user`-objektet, kan man bruke `repLogger2`:
```R
rapbase::repLogger2(user = user, msg = "Tekst som logges")
```
Da vil det også logges hvilken rolle og hvilken enhet man har ved loggtidspunktet.

## Hvor lagres logg?

Det er etablert en MySQL‑database på NHN for logging fra Rapporteket‑applikasjonene. Alle applikasjoner har `SELECT`‑ og `INSERT`‑rettigheter til denne databasen. I tillegg til logging til database, logges det til NHNs interne loggsystemer. Der logges også all standard output (stdout) og standard error (stderr).

