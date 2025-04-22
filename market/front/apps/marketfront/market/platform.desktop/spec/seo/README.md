# Интеграционные SEO-тесты

## Разработка

```bash
INTEGRATION_TEST=true npm run test:jest:seo
```

Если нужно проверить на каком-то стенде, то надо добавить `BASE_URL`:
```bash
BASE_URL=https://front-market--marketfront-6897-dsk.demofslb.market.yandex.ru INTEGRATION_TEST=true npm run test:jest:seo
```

Чтоб прогнать тесты на другом кадавре, надо добавить `kadavr_host` и `kadavr_port` (без флага `INTEGRATION_TEST=true`):
```bash
kadavr_host=kadavr.vs.market.yandex.net kadavr_port=80 npm run test:jest:seo
```

## Структура тестов

Тесты разбиты на страничные папки
```
suites
│
└───ProductPage  # страница /product--<slug>/<id>
│   │    redirects.spec.js
│   │    ...
│
└───CatalogListPage  # страница /catalog--<slug>/<nid>/list
│   │   redirects.spec.js
│   │   ...
│
│   ...
```
