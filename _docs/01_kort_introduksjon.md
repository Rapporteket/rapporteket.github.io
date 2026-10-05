---
layout: page
title: "Kort om Rapporteket"
nav_order: 1
permalink: /rapporteket
---

*Rapporteket* er en analyse- og rapporteringstjenste som benyttes av medisinske kvalitetsregistre.
Medisinske kvalitetsregistre har som formål å overvåke kvalitet og bidra til kvalitetsforbedring i helsetjenesten.
Med utgangspunkt i data fra registrene kan *Rapporteket* tilby interaktiv undersøkelse av rådata, rutinemessig utsending av rapporter og visualisering av resultater fra registrene.
Tjenesten utvikles og vedlikeholdes av [Nasjonalt servicemiljø for medisinske kvalitetsregistre](https://www.kvalitetsregistre.no/) ved [Senter for Klinisk Dokumentasjon og Evaluering (SKDE)](https://www.skde.no/).

Teknologien bak *Rapporteket* er i hovedsak basert på statistikkprogrammet [R](https://www.r-project.org/) og webpubliseringsverktøyet [Shiny](https://shiny.posit.co/), som er fritt tilgjengelig programvarem for statistiske og grafiske formål.
All programkode og annet innhold (utenom registerdata) på *Rapporteket* er strukturert i [R-pakker som lages og vedlikeholdes av statistikere i registrene og i Servicemiljøet](https://github.com/Rapporteket).

Resultatene genereres på grunnlag av data tilgjengelig fra Registerets database. 
Resultater vil i denne sammenheng først og fremst være figurer og tabeller som oppsummerer data hentet fra registerets datakilde.
Det kan også være ferdige rapporter i form av et dokument med figurer, tabeller og analyser.
Rapporter kan settes opp til å sendes ut regelmessig  på e-post.

_Eksempler på resultater, visualiseringer og funksjonalitet Rapporteket-applikasjonen til et register kan inneholde:_

* Figurer hvor man kan gjøre ulike datautvalg, eksempelvis fordeling av en variabel, utvikling over tid (per måned/år) eller figurer som sammenligner resultater fra hvert av sykehusene. 
* Registreringsoversikter, status
* Tabelloversikter, nøkkeltall
* Dashboard - samling/sammenstilling av oppdatert nøkkelinforasjon for registeret på én side.
* Samlerapport med figurer/tabeller og tekst som brukeren kan laste ned fra Rapporteket eller få tilsendt på e-post. Registeret  definerer innholdet i samlerapporten (figurer, tabeller, analyser og tekst), hvilket utvalg rapporten skal gjelde og hvor ofte den skal sendes ut. Rapporten er til en hver tid oppdatert med alle data som er overført til Rapportekets database.  
