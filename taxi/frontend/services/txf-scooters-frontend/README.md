# Фронтенд самокатов

|                                                                                                                                               Last pre-release                                                                                                                                               |                                                                                                                                                                                                                                                                                                              Last unstable |
| :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
| [![Build Status](https://teamcity.taxi.yandex-team.ru/app/rest/builds/buildType:YandexTaxiProjects_FrontendMonorepo_Stable,branch:txf-scooters-frontend/statusIcon)](https://teamcity.taxi.yandex-team.ru/viewType.html?buildTypeId=YandexTaxiProjects_FrontendMonorepo_Stable&branch=txf-scooters-frontend) | [![Build Status](https://teamcity.taxi.yandex-team.ru/app/rest/builds/buildType:YandexTaxiProjects_Infranaim_Frontend_NewFlowTest,branch:txf-scooters-frontend/statusIcon)](https://teamcity.taxi.yandex-team.ru/viewType.html?buildTypeId=YandexTaxiProjects_Infranaim_Frontend_NewFlowTest&branch=txf-scooters-frontend) |

-   [Сервис в админке](https://tariff-editor.taxi.yandex-team.ru/services/43/edit/356310/info)
-   [Переводы](./.tanker/README.md)

## Логи

| name                    | url                                                                                                                                                                                                                                                                                                                       |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| kibana testing (nodejs) | [log](<https://kibana.taxi.tst.yandex-team.ru/app/kibana#/discover?_g=(refreshInterval:(pause:!t,value:0),time:(from:now-15m,to:now))&_a=(columns:!(_source),index:'1df0b0f0-b956-11e9-9ad8-afd09b0ebd4e',interval:auto,query:(language:kuery,query:'name:%20taxi-txf-scooters-frontend'),sort:!(!('@timestamp',desc)))>) |
| kibana stable (nodejs)  | [log](<https://kibana.taxi.yandex-team.ru/app/kibana#/discover?_g=()&_a=(columns:!(_source),index:f8e70880-c75c-11e9-8a12-ddb2ef5a51ea,interval:auto,query:(language:kuery,query:'name:%20taxi-txf-scooters-frontend'),sort:!(!('@timestamp',desc)))>)                                                                    |
| error-booster (browser) | [log](https://error.yandex-team.ru/projects/taxi-scooters-frontend/projectDashboard)                                                                                                                                                                                                                                      |

## Метрики

| name                       | url                                                                                                        |
| -------------------------- | ---------------------------------------------------------------------------------------------------------- |
| grafana (testing)          | [url](https://grafana.yandex-team.ru/d/WoJojkd7z/nanny_taxi_scooters-frontend_testing?orgId=1&refresh=30s) |
| grafana (stable)           | [url](https://grafana.yandex-team.ru/d/0AxK3kd7k/nanny_taxi_scooters-frontend_stable?orgId=1&refresh=30s)  |
| rum (browser, performance) | [url](https://error.yandex-team.ru/projects/taxi-scooters-frontend/projectDashboard)                       |

## URLs

| name            | testing                                                 | stable                                         |
| --------------- | ------------------------------------------------------- | ---------------------------------------------- |
| Вебвью подписки | https://m.taxi.taxi.tst.yandex.ru/scooters/subscription | https://m.taxi.yandex.ru/scooters/subscription |

### Авторизация

`x-yataxi-userid` и `Session_id` (паспортной куке)

### GET-параметры

- `position` (`=lon,lat`) текущая позиция пользователя

## Установка и разработка

Создать сертификат [тут](https://crt.yandex-team.ru/certificates) и положить в папку проекта `certs/dev.pem`

<details>
  <summary>Как заполнить формочку</summary>

-   CA Name: InternalCA
-   ABC-Сервис: Сервисы Такси
-   Хосты: localhost.msup.yandex.ru

</details>

```
nvm use
```

> Иначе зайти в .nvmrc и установить в ручную

```
npm ci
npm start
```

## Сборка

```
npm run build
```

## Релиз

[Как собирать и катить релиз](https://wiki.yandex-team.ru/taxi/efficiency/dev/frontend/rtc/fast-create-service/#razrabotka)

## Разное

[Расширение для подмены заголовков](https://chrome.google.com/webstore/detail/modheader/idgpnmonknjnojddfkpgkljpfnnfcklj?hl=ru)
