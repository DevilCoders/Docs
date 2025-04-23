# Резолвер resolveOffersByIds

Резолвер, который возвращает офферы по wareId.
Данные в ответе резолвера нормализованы.

## Параметры

| Parameter | Type | Description | Default |
|---------------|----------|------------------|------------------|
| `offerIds`* | array | Массив id офферов | - |
| `pp` | string |  Идентификатор места показа | 'DEFAULT' |
| `cpc` | OfferShowPlaceId| Сущность, в которую вынесены поля, содержащие статистические данные оффера и нижележащих сущностей | - |
| `pickup-options` | string | Флаг, включающий вывод опций самовывоза для доставки. | - |
| `referer` | string | Полный урл запрошенной страницы. | - |
| `regset` | number | Фильтрация предложений из других регионов. | - |
| `clid` | number|  | - | - |

Более подробное описание параметров – https://wiki.yandex-team.ru/market/verstka/report-query-params/

\* - обязательный параметр

## Пример ответа резолвера
```json
{
  "results": [
    {
      "handler": "resolveOffersByIds",
      "result": "jfgqorvl0d"
    }
  ],
  "collections": {
    "searchResult": "Array()",
    "visibleEntity": "Array()",
    "offerShowPlace": "Array()",
    "offer": "Array()"
  }
}
```

## Ссылки

- [Формат возвращаемых данных](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/api/app/handlers/resolveOffersByIds/v1/index.js#L20)
- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/resolvers/offers/resolveOffersByIds.js#L10)
- [Микроформат сущности](https://github.yandex-team.ru/market/microformats/blob/master/offer/offer.json)
- [Описание сущности `оффер` в проекте](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/entities/offer/index.js)
- [Список констант параметра `PP`](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/entities/report/constants.js#L9)
