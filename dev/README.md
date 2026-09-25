## Lokal utvikling og testing

Sidene kan bygges og testes lokalt i et utviklingsmiljø med code-server (vscode).

- Kjør opp code-server med docker-compose fra `dev/`-mappen (`cd dev && docker compose up`)
- Åpne mappen */config/workspace/rapporteket.github.io* inne i code-server
- Åpne terminal i code-server
- Bygg (`bundle install`)
- Serve (`bundle exec jekyll serve --host 0.0.0.0`)
- Se ved å gå til http://localhost:4000/. Her vil du sannsynligvis havne på `http://localhost:8443/proxy/4000/`. Da fjerner du bare `8443/proxy/` i url-en.
