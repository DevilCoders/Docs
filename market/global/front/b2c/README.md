# Global Market B2C Superapp

Документация по разработке на [Вики](https://wiki.yandex-team.ru/lavka/dev/front/monorep/)

## Хосты

[Сервис grocery-superapp](https://tariff-editor.taxi.yandex-team.ru/services/35/edit/355571/info)


## Установка и разработка

```bash
cd services/lavka-grocery-superapp/
npm ci
npm run dev
arc checkout -b lavka-grocery-superapp/LAVKAFRONT-XXX
```

## Сборка

- `npm run build:{ENV}` — ENV: stable | testing | unstable

## Релиз

[Как собирать и катить релиз](https://wiki.yandex-team.ru/taxi/efficiency/dev/frontend/rtc/fast-create-service/#razrabotka)


## Полезно знать

* [Установка Arc](https://docs.yandex-team.ru/devtools/intro/quick-start-guide)
* [GAP конфиг в проде](https://tariff-editor.taxi.yandex-team.ru/authproxies/grocery-authproxy/show/LzQuMC9ncm9jZXJ5LXN1cGVyYXBwL2xhdmth)
* [Сервис grocery-superapp в админке](https://tariff-editor.taxi.yandex-team.ru/services/35/edit/355571/info)
* [Эксперименты в проде](https://tariff-editor.taxi.yandex-team.ru/experiments3/experiments?enabled=enabled&active=active&order=action_from__action_to&consumers=lavka-frontend)
* [Конфиги в проде](https://tariff-editor.taxi.yandex-team.ru/experiments3/configs?enabled=enabled&active=active&order=action_from__action_to&consumers=lavka-frontend)
* [Работа с танкером](https://github.yandex-team.ru/taxi/frontend-monorepo/blob/master/services/lavka-grocery-superapp/.tanker/README.md)
