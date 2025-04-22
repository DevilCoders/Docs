# github-token-proxy

Образ контейнера с `proxy`, добавляющим токен при обращении к `github`.

Этот прокси-сервер используется при выставлении статусов `github` из задач `sandbox`, выполняющихся на `sandbox`-сервере
(например, хук `on_enqueue`).

Прокси не требует своей авторизации, но проксирует только запросы на выставление статусов проверок на `github`.
В данный момент проксируются только запросы на установку статусов ```/repos/:owner/:repo/statuses/:sha```
Документация по этому api: https://developer.github.com/enterprise/2.11/v3/repos/statuses/

Исходная задача: https://st.yandex-team.ru/FEI-10158

## Разработка

`npm run start` - запуск dev-сервера, запускает сборку
`npm run stop` - остановка dev-сервера
`npm run build` - сборка образа с тегом `dev`

## Сборка и обновление

```
npm run build
docker tag registry.yandex.net/search-interfaces/github-token-proxy:dev registry.yandex.net/search-interfaces/github-token-proxy:latest
docker push registry.yandex.net/search-interfaces/github-token-proxy:latest
```

Прокси поднят в https://deploy.yandex-team.ru/project/github-token-proxy
