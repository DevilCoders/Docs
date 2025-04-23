# Services

### http-gvm-proxy-nginx
http-сервер, которые терминирует TLS и проксирует запрос в http-gvm-proxy.
Чтобы сервис запустился нормально нужно подложить `certificate.crt` и `private.key` в `~/.gvm_compose/nginx`.

# Development
### Circumstances
* openvas-scanner requires `--network host` и `--privileged`.
* exposing ports: `gsad - 50000, http-gvm-proxy - 50002, http-gvm-proxy-nginx - 50003`
### Steps
1. Start services `docker compose --profile http-gvm-proxy up -d`.

# Deployment

### Nessus

##### Circumstances
* Docker/Compose networking fails to expose ports. So we have to use host network with `network_mode: host` for compose or `--network host` for docker run.
* Try to prevent listen port intersection with other services on a system. `gsad - 50000, gvmd - 50001, http-gvm-proxy - 50002, http-gvm-proxy-nginx - 50003, postgres - 50009`.
* Need to prepare some secrets for TLS.

##### Steps
1. Put `certificate.crt`, `private.key` in `~/.gvm_compose/gsad/`.
2. Put `certificate.crt`, `private.key` in `~/.gvm_compose/nginx/`.
3. Copy postgres config from `gvm-postgres/nessus-postgres.conf` to `~/.gvm_compose/postgres/postgresql.conf`.
4. Set env var for `GVMD_PASSWORD`.
5. Start services `docker compose --profile http-gvm-proxy -f docker-compose.yml -f docker-compose.nessus.yml up -d`.
