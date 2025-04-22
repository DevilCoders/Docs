# FAPI

## Документация

[Ссылка на Swagger](https://marketfront.s3.mds.yandex.net/arcadia-ci/fapi-docs/index.html)

## Описание

Frontend/Front API. Набор endpoint'ов (handler'ов),
которые предоставляют доступ мобильным приложениям к резолверам синего фронта

[Архитектура](https://wiki.yandex-team.ru/Market/frontend/apiary/frontend-api/)

## Старт

Для сборки из корня платформы (`api`) выполни:
1. `npm run make:all`

Для запуска из корня платформы (`api`) выполни:
1. `npm run start:debug`

- Доступ в проде: `https://ipa.market.yandex.ru` (ipa!)
- Доступ на разработческом стенде: `https://<username>.api.logrus01ed.market.yandex.ru` (api!)

Для разработки запусти:
1. `npm run webpack:watch`

Очистка проекта:
1. `npm run clean`


## Создание Хэндлера
Предпочтительно использовать [генератор](https://github.yandex-team.ru/market/generator-market)
`yo market:fapi -f`


## Структура

Ручки FAPI определены в мандреле (`@yandex-market/mandrel/routes.js.flow`). Сейчас их две:

1. `/doc/v<version>` - WIP. Будет отдавать документацию по указанной версии fapi.
1. `/api/v<version>` - POST-ручка для доступа к handler'ам указанной версии.
- В качестве параметров передаётся
    - `name` - список имен handler'ов
- В качестве заголовков необходимо передать
    - `X-Region-id` - форсировано проставит регион пользователя, которое приложение знает лучше `nodules`
    - `api-platform: ANDROID` / `api-platform: IOS`
    - `Content-Type: application/json`
    - `X-User-Authorization: OAuth <OAuth Token>` - если ручке требуется авторизация
- В теле запроса обязательно надо указать
    - Массив объектов параметров каждого из указанных в параметре `name` handler'ов

Контроллер FAPI лежит в мандреле: `@yandex-market/mandrel/pages/FrontApiPage`;

Handler'ы определены в проекте, в `api/app/handlers`.

## Пример запроса

```bash
curl -X POST \
  'https://ipa.market.yandex.ru/api/v1?name=resolveSku' \
  -H 'Content-Type: application/json' \
  -H 'X-User-Authorization: OAuth AQAAAADu-WeeAAAKiYi-bmjyjUb0ikd4i28BWUk' \
  -H 'api-platform: ANDROID' \
  -H 'cache-control: no-cache' \
  -d '{
 "params": [
  {
   "skuId":100244446725,
   "billingZone": "skuCard"
  }
 ]
}
'
```

## Тесты

[Интеграционные](https://a.yandex-team.ru/arc_vcs/market/front/apps/marketfront/api/__integration__/README.md)

## Авторизация

[Как получить OAuth токен](https://wiki.yandex-team.ru/market/beru/front/fapi-beru/kak-poluchit-token-dlja-fapi/)
