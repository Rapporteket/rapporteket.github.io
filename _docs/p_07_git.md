---
layout: page
title: "Hvordan jobber vi med Git/Github"
---

Mer generell informasjon om hvordan man jobber med Git og Github finnes ikke her.
Dette er ment som en kort innføring i hvordan vi i Rapporteket jobber med kildekode og versjonskontroll.
For mer generell informasjon om Git og Github, se [Pro Git-boken](https://git-scm.com/book/en/v2) eller [Github Docs](https://docs.github.com/en).
For enklere introduksjon til Git se f.eks. [software carpentry](https://swcarpentry.github.io/git-novice/) eller søk på nett.
[Learn Git Branching](https://learngitbranching.js.org/) er også en fin interaktiv måte å lære Git på.
Hvis du foretrekker video kan du sjekke ut [*Git for Ages 4 and Up*](https://www.youtube.com/watch?v=1ffBJ4sVUb4).

## Forvaltning av kildekode 

Kildekode til alle egenutviklede rapportek-applikasjoner ligger åpent på [github](https://github.com/Rapporteket), som regel med lisensen [GNU General Public License 3](https://www.gnu.org/licenses/gpl-3.0.en.html).

I alle depoene (*repositories*) er det én hovedgren: `main`.
Denne grenen skal alltid være klar for å deploye til produksjon.
Når en ny versjon lages i github, brukes [Semantic Versioning](https://semver.org/) for å navngi versjonen.
Når en ny versjon lages, vil denne automatisk bygge og deploye docker image med applikasjonen til NHN.
For mer informasjon om å få ny versjon opp på NHN, se [egen side om hvordan man publisere ny versjon](p_04_ny_release.html).

## *Pull requests*

Grenen `main` er i alle depoer beskyttet for direkte *commits*. Alle endringer må gjennom en *pull request* (PR) for å komme inn i `main`.
For at kode skal komme inn i `main` må ingen av testene feile og koden må gjennom en *code review* (fagfellevurdering) av ett av medlemmene på Rapporteket.
For å lage en ny PR basert på `main` kan man gjøre følgende lokalt i terminal:

```sh
git status # sjekk at alt ser rent og pent ut (ingen filer som ikke er staged eller commited)
git switch main # gå inn i hovedgrena (samme som git checkout main)
git pull # hent ned siste endringer
git switch -c <new_branch> # lag (c for create) og bytt til ny gren (bruk annet navn enn <new_branch>)
# ...
# gjøre endringer i koden
# ...
git status # se hvilke filer som er endret
git add <filenames> # stage filer. "git add ." vil legge til alle filer, men pass på at ikke filer du ikke vil legge opp på github blir med her.
git status # se hvilke filer som er staget
git commit -m "Fornuftig commit-beskjed" # skriv litt prosa om hva som er gjort
git push -u origin <new_branch> # dytt opp til Github (bytt ut <new_branch> med navnet du ga tidligere)
# Lag en PR, enten gjennom lenke som dukker opp i terminalen eller ved å gå til Github-repoet og se etter knapp.
```
Alt dette kan eventuelt gjøres gjennom knapper i RStudio eller Visual Studio Code.

## Hvem kan endre koden

Kun [medlemmer av *Rapporteket* på github](https://github.com/orgs/Rapporteket/people) kan dytte opp endringer direkte til en gren på https://github.com/Rapporteket.
Unntaket er `main`-grenen, der kun administratorene kan dytte opp endringer direkte.
 Det er fåtall som har administratorrettigheter.
 De som ikke er medlemmer av `Rapporteket` må lage en *fork* av koden og foreslå endringer til `main` gjennom denne *forken*.
