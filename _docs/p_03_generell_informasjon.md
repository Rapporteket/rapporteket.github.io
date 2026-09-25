---
layout: page
title: "Rapporteket, generell informasjon"
nav_order: 3
permalink: /om
---

Rapporteket er en elektronisk resultattjeneste som er tilgjengelig for medisinske kvalitetsregistre. For mer informasjon om Rapporteket, se [kvalitetsregistre.no](https://www.kvalitetsregistre.no/formidling/rapporteket)

## Innhold

Rapporteket er bygd opp ved hjelp av  statistikkprogrammet R og webpubliseringsverktøyet Shiny. 
All programvare er basert på åpen kildekode.
R-koden, som danner grunnlaget for registerets Rapporteket-applikasjon, finnes på https://github.com/Rapporteket.
Hvert register har sin egen Rapporteket-applikasjon.

Resultatene genereres på grunnlag av data tilgjengelig fra Registerets database. 
Resultater vil i denne sammenheng først og fremst være figurer og tabeller som oppsummerer data hentet fra registerets datakilde.
Det kan også være ferdige rapporter i form av et dokument med figurer, tabeller, analyser og tekst (prosa).
Rapporter kan settes opp til å sendes ut regelmessig  på e-post.

_Eksempler på resultater, visualiseringer og funksjonalitet Rapporteket-applikasjonen til et register kan inneholde:_

* Figurer hvor man kan gjøre ulike datautvalg, eksempelvis fordeling av en variabel, utvikling over tid (per måned/år) eller figurer som sammenligner resultater fra hvert av sykehusene. 
* Registreringsoversikter, status
* Tabelloversikter, nøkkeltall
* Dashboard - samling/sammenstilling av oppdatert nøkkelinforasjon for registeret på én side.
* Samlerapport med figurer/tabeller og tekst som brukeren kan laste ned fra Rapporteket eller få tilsendt på e-post. Registeret  definerer innholdet i samlerapporten (figurer, tabeller, analyser og tekst), hvilket utvalg rapporten skal gjelde og hvor ofte den skal sendes ut. Rapporten er til en hver tid oppdatert med alle data som er overført til Rapportekets database.  
