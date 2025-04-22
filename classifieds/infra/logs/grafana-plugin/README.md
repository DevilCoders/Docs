# Vertis-Logs Grafana Data Source Plugin

Display history and realtime vertis logs.

## Getting started
1. Install dependencies
```BASH
yarn install
```
2. Build plugin in development mode or run in watch mode
```BASH
yarn dev
```
or
```BASH
yarn watch
```
3. Up docker image
```BASH
docker-compose up -d
```
4. Build plugin in production mode
```BASH
yarn build
```

## Development
Для того чтобы разрабатывать с нормальными данными надо добавить datasource в настройках (графана изначально поднимается пустая)
`Configuration -> Data Sources -> Add data source`

Чтобы упростить разработку, можно настроить IDE для запуска линтера с корректным набором правил:
![eslint ide config](./eslint.png)

## Deploy
- Обновить версию в package.json
- `VERSION=<version> GRAFANA_API_KEY=<key> make release`
  * `version` - версия из package.json
  * `key` - ключ от API, https://yav.yandex-team.ru/secret/sec-01ezf9ncc4w4dz1a322bp3ryvh/explore/versions
- Обновить версию в [Dockerfile grafana](https://a.yandex-team.ru/arc/trunk/arcadia/classifieds/infra/admin-dockerfiles/grafana/Dockerfile?rev=r9310514#L13)
- Сбилдить обновленный образ графаны https://t.vertis.yandex-team.ru/project/VertisAdmin_GrafanaDockerBuild?mode=builds
- Выкатить:
  - `testing` https://admin.vertis.yandex-team.ru/services/grafana-test
  - `prod` https://admin.vertis.yandex-team.ru/services/grafana
- Графана доступна по адресам:
  - `testing` https://grafana.test.vertis.yandex-team.ru 
  - `prod` https://grafana.vertis.yandex-team.ru 

## Learn more
- [Build a data source plugin tutorial](https://grafana.com/tutorials/build-a-data-source-plugin)
- [Grafana documentation](https://grafana.com/docs/)
- [Grafana Tutorials](https://grafana.com/tutorials/) - Grafana Tutorials are step-by-step guides that help you make the most of Grafana
- [Grafana UI Library](https://developers.grafana.com/ui) - UI components to help you build interfaces using Grafana Design System
