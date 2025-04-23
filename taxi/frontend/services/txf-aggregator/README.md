# Фронтенд сервиса Кабинет агрегатора

**Сборки**

| Service | Last pre-release | Last unstable |
| :-------------- | :--------------: | ------------: |
|  | [![Build Status](https://teamcity.taxi.yandex-team.ru/app/rest/builds/buildType:YandexTaxiProjects_FrontendMonorepo_Stable,branch:txf-aggregator/statusIcon)](https://teamcity.taxi.yandex-team.ru/viewType.html?buildTypeId=YandexTaxiProjects_FrontendMonorepo_Stable&branch=txf-aggregator) | [![Build Status](https://teamcity.taxi.yandex-team.ru/app/rest/builds/buildType:YandexTaxiProjects_Infranaim_Frontend_NewFlowTest,branch:txf-aggregator/statusIcon)](https://teamcity.taxi.yandex-team.ru/viewType.html?buildTypeId=YandexTaxiProjects_Infranaim_Frontend_NewFlowTest&branch=txf-aggregator) | 

**Error logs**

| Service | stable | testing | client |
| :-------------- | --------------: | --------------: | ------------: |
|   | [stable](https://kibana.taxi.yandex-team.ru/app/kibana#/discover?_g=(refreshInterval:(pause:!t,value:0),time:(from:now-60m,to:now))&_a=(columns:!(_source),index:'1df0b0f0-b956-11e9-9ad8-afd09b0ebd4e',interval:auto,query:(language:kuery,query:'name:%20txf-aggregator'),sort:!(!('@timestamp',desc)))) | [testing](https://kibana.taxi.tst.yandex-team.ru/app/kibana#/discover?_g=(refreshInterval:(pause:!t,value:0),time:(from:now-60m,to:now))&_a=(columns:!(_source),index:'1df0b0f0-b956-11e9-9ad8-afd09b0ebd4e',interval:auto,query:(language:kuery,query:'name:%20txf-aggregator'),sort:!(!('@timestamp',desc)))) | [тут](https://error.yandex-team.ru/projects/taxi-aggregator/projectDashboard) |

**hosts**

| Service | stable | testing |
| :-------------- | :-------------- | ------------: |
|  | [agg.taxi.yandex.net](https://agg.taxi.yandex.net)<br/>[agg.taximeter.yandex.ru](https://agg.taximeter.yandex.ru)<br/>[aggregator.taxi.yandex.net](https://aggregator.taxi.yandex.net) | [agg.taxi.tst.yandex.net](https://agg.taxi.tst.yandex.net)<br/>[aggregator.taxi.tst.yandex.net](https://aggregator.taxi.tst.yandex.net) | 

#### разработка

**Сервис разрабатывается на дев машинках [QYP](https://wiki.yandex-team.ru/taxi/web/yp-frontend-guide/)**

Маутим [аркадию](https://docs.yandex-team.ru/devtools/intro/quick-start-guide#system-requirements) в ~ на машинке. Должен получиться путь `~/arc/arcadia/taxi/frontend`. Если у вас проект лежит в другой папке - порпавьте файлы nginx сервиса

**Важно:** Маутнить аркадию надо с флагом --allow-other, но для его спервать дать права на fuse конфиг

```(bash)
addgroup <username> fuse
arc mount --allow-other -m arcadia/ -S store/
```

## Установка и разработка

- `cd services/txf-aggregator/`
- `npm run install`
- `npm run run`

## Сборка

- `npm run build:{ENV}` — ENV: stable | testing | unstable

## Релиз

[Как собирать и катить релиз](https://wiki.yandex-team.ru/taxi/efficiency/dev/frontend/rtc/fast-create-service/#razrabotka)

## Метрика

https://metrika.yandex.ru/dashboard?group=dekaminute&period=yesterday&id=74420146
