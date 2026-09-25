# rapporteket.github.io
Oppdatert informasjon om Rapporteket

## Lokal testing av sidene med docker

- Kjør opp code-server med docker-compose fra `dev/`-mappen (`cd dev && docker compose up`)
- Åpne mappen *rapporteket.github.io* inne i code-server
- Åpne terminal i code-server
- Bygg (`bundle install`)
- Serve (`bundle exec jekyll serve --host 0.0.0.0`)
- Se ved å gå til http://localhost:4000/
