---
layout: page
title: "Rapporteket som containerapplikasjon"
nav_order: 20
permalink: /docker
---

- TOC
{:toc}

## Kort introduksjon

Siden 2025 har Rapporteket blitt levert som frittstående containerapplikasjoner driftet i et [Kubernetes](https://kubernetes.io/)-klyngemiljø.
Dette dokumentet foreslår metoder som skal bidra til en smidig og robust prosess fra utvikling til produksjonssetting gjennom hele applikasjonens livssyklus.

## Containerinnhold

I denne løsningen representeres hvert register som en selvstendig containerapplikasjon i Rapporteket, det vil si at utrulling baseres på registerspesifikke containerbilder.

Samtidig deler alle registre i Rapporteket et felles sett med funksjoner, som systemmiljø og underliggende programvare. Disse etableres i et grunnleggende containerbilde som alle registerspesifikke containerbilder bygges på. Begge typer containerbilder beskrives nedenfor.

### Grunnleggende containerbilde

Det finnes to grunnleggende image, [base-r](https://github.com/Rapporteket/docker/blob/main/base-r/Dockerfile) og [base-r-alpine-latex](https://github.com/Rapporteket/docker/blob/main/base-r-alpine-latex/Dockerfile). Ett er basert på *Ubuntu Linux* og ett er basert på *Alpine Linux*. Begge disse inneholder felles systembiblioteker, den gjeldende stabile R-versjonen (*R-release*) og et sett med felles R-pakker.

Utgangspunktet for Ubuntu-bildet er [rocker/r-ver](https://rocker-project.org/images/versioned/r-ver.html), som følger utviklingen av Ubuntu LTS. Utgangspunktet for Alpine-bildet er [rhub/r-minimal](https://github.com/r-hub/r-minimal). Begge følger utviklingen av R-release. Det vil si at versjonsnummeret til bildet tilsvarer R-versjonen.

### Applikasjonscontainerbilde

Registerenes R Shiny-applikasjoner legges oppå ett av de grunnleggende containerbildene (se over). Kildekoden for hver registerapplikasjon forvaltes i [Rapporteket-organisasjonen på GitHub](https://github.com/Rapporteket), hvor bygging av disse bildene ligger. En typisk `Dockerfile` ser slik ut:

```docker
FROM rapporteket/base-r:main

WORKDIR /app/R

RUN --mount=type=secret,id=github_pat,env=GITHUB_PAT \
    --mount=type=bind,source=.,target=/app/R/pkg \
    R -e "remotes::install_local(path = './pkg')"

EXPOSE 3838

RUN adduser --uid 1000 --disabled-password rapporteket && \
    chown -R 1000 /app/R && \
    chmod -R 755 /app/R
USER 1000

CMD ["R", "-e", "options(shiny.port = 3838, shiny.host = \"0.0.0.0\"); packageName::run_app()"]
```


## Pipeline for kontinuerlig integrasjon og leveranse (CI/CD)

For å sikre at endringer i applikasjonene i Rapporteket kan leveres på en rask og pålitelig måte, benyttes definerte arbeidsflyter. 

### CI/CD-verktøy og metoder

Siden alle kodearkiver forvaltes på GitHub, benyttes [GitHub Actions](https://docs.github.com/en/actions) til å håndheve retningslinjer og kjøre CI/CD-oppgaver. Disse oppgavene utføres både etter faste tidsplaner og som respons på foreslåtte kodeendringer.

### Utrulling (Deployment)

I første trinn merkes den aktuelle applikasjonskoden med en utgivelsesversjon (*release*) fra `main`-grenen, og et nytt bilde bygges og distribueres til NHN automatisk. 
Denne applikasjonen legges i et kvalitetssikringsmiljø (QA) for funksjonell testing.
Etter vellykket testing distribueres bildet til produksjonsmiljøet.
Prosessen er ytterligere beskrevet i kapitlet [Hvordan publisere ny versjon av en Rapporteket-applikasjon](/release).

### Sårbarhetsskanning

Overvåking av containerbilder utføres med [Trivy](https://trivy.dev/). Grunnbildet overvåkes gjennom ukentlige skanninger for å avdekke nye trusler. Endringer i den underliggende koden skannes også som en del av alle *pull requests* for å hindre at nye sårbarheter introduseres i hovedprosjektet.

For tiden aksepteres sårbarheter med lav, moderat eller høy alvorlighetsgrad, mens sårbarheter med kritisk alvorlighetsgrad ikke aksepteres.
