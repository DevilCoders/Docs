# Резолвер resolveSearch

Возвращает выдачу репорта из метода `prime`.
**Не умеет в редиректы** на каталог, редиректы должны хэндлиться на клиенте.
Данные в ответе резолвера нормализованы.

## Параметры

| Parameter | Type | Description | Default | Value |
|---------------|----------|------------------|------------------| ------- |
| `text`* | string | Поисковый запрос пользователя | - | - |
| `page`** | number |  Номер страницы | 1 | - |
| `how` | string| Тип сортировки | - | - |
| `hid`* | number| Идентификатор товарного дерева | - | - |
| `nid` | number| Идентификатор навигационного дерева | - | - |
| `filters` | Object(Array/string) | Фильтры (см. `constraints`) | - | - |
| `searchPlace` | string| Плейс репорта | - | - |
| `show-offers` | string|  | - | - |
| `use-default-offers` | string|  | - | - |
| `isMultisearch` | boolean|  | - | - |
| `clid` | number|  | - | - |
| `pickup-options` | `'grouped' | 'raw'` | Вид представления самовывоза | - |
| `prime-output` | number | Скрытие результатов поиска:<br> 0 — фильтры + результаты<br> 1 —  в выдаче будут только фильтры (это быстрее, чем возвращать полный результат)<br> 2 — только результаты | 0 | [0, 1, 2] |
| `pp` | string | Место показа. [Список ключей](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/entities/report/constants.js#L122-L154) | - |

\* - обязательно наличие хотя бы одного параметра

\** - обязательный параметр

## Пример ответа резолвера
```json
{
  "results": [
    {
      "handler": "resolveSearch",
      "result": "oe222y80v8"
    }
  ],
  "collections": {
    "visibleSearchResult": [
      {
        "id": "oe222y80v8",
        "text": "iphone 10",
        "page": 1,
        "searchResultIds": {
          "1": "mz1yqncc1p"
        },
        "sortId": "aprice",
        "sortIds": "Array()",
        "filterIds": "Array()",
        "intentIds": "Array()"
      }
    ],
    "searchResult": [
      {
        "id": "mz1yqncc1p",
        "visibleEntityIds": [
          "productShowPlace_1759344092_15802173990375625061216001",
          "productShowPlace_217317885_15802173990375625061216002",
          "productShowPlace_92352002_15802173990375625061216003",
          "productShowPlace_71309158_15802173990375625061216004",
          "productShowPlace_217312163_15802173990375625061216005",
          "productShowPlace_217312269_15802173990375625061216006",
          "productShowPlace_14206636_15802173990375625061216007",
          "productShowPlace_217312280_15802173990375625061216008",
          "productShowPlace_217311018_15802173990375625061216009",
          "productShowPlace_217320262_15802173990375625061216010"
        ]
      }
    ],
    "visibleEntity": "Array()",
    "productShowPlace": "Array()",
    "product": "Array()",
    "offerShowPlace": "Array()",
    "offer": "Array()"
  }
}
```

## Ссылки

- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/api/app/handlers/resolveSearch/v2/index.js)
- [Микроформат сущности](https://github.yandex-team.ru/market/microformats/blob/master/search/search.json) (**WARNING**: микроформат устаревший и может не соответствовать действительности.)
- [Описание сущности `visibleSearchResult` в проекте](https://github.yandex-team.ru/market/marketfront/blob/master/market/src/entities/visibleSearchResult/index.js#L20)
- [Описание схемы нормализации поискового ответа](https://wiki.yandex-team.ru/market/frontend/conventions/#pokaztovarov) (у нас аналогично синему, но без сущности SKU)
