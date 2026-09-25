---
layout: page
title: "Hvordan publisere ny versjon av en Rapporteket-applikasjon"
nav_order: 4
---

1. Lag en ny versjon på github.
   - Gå inn på *releases* på høyre side, som fører deg til github.com/Rapporteket/\<ditt rapportek\>/releases

     ![Skjermbilde av github-nettside, gå til release](/img/go-to-release.png)

   - Trykk på *Draft a new release* øverst til høyre, som fører deg til github.com/Rapporteket/\<ditt rapportek\>/releases/new

     ![Skjermbilde av github, lag ny release](/img/draft-new-release.png)

   - Trykk på *Choose a tag* og skriv inn neste versjonsnummer, f.eks. `v1.2.0` (vi bruker [semver](https://semver.org/) for hvordan vi setter versjonsnummer). Versjonsnummeret skal være hakket over forrige versjon, og det skal lages en ny tag (trykk på *Create new tag: v1.2.0 on publish*)

     ![Skjermbilde av github-nettside, lag ny tag](img/create-new-tag.png)

   - Sjekk at du har valgt riktig gren (f.eks. *Target: main*)

     ![Skjermbilde av github-nettside, sjekk branch](/img/target-branch.png)

   - Trykk på *Generate release notes*.

     ![Skjermbilde av github-nettside, lag release-notes](/img/generate-release-notes.png)

   - Trykk på *Publish release*.

     ![Skjermbilde av github-nettside, publiser](/img/publish-release.png)

2. Vent til ny versjon er dyttet opp til Harbor. Sjekk status under github.com/Rapporteket/\<ditt rapportekt\>/actions.
3. Endre til nytt versjonsnummer i fila `values-qa.yaml` i qa på [helsegitlab](https://helsegitlab.nhn.no/team-register/rapporteket/rapporteket). 
*Eksempel:* image: ncr.sky.nhn.no/rapporteket/intensiv:3.1.19 -> image: ncr.sky.nhn.no/rapporteket/intensiv:3.1.20
Vent noen minutter på at ny versjon dukker opp på [rapporteket.qa.nhn.no/app/\<ditt rapportekt\>](https://rapporteket.qa.nhn.no/).
4. **Sjekk applikasjonen nøye.**
5. Hvis alt er OK, opprett en *merge request* mot prod-grena ved å gjøre tilsvarende endring i `values-prod.yaml` som ble gjort i punkt 3.
