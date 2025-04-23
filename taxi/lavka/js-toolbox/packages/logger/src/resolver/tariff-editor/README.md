## [Поля кибаны](https://a.yandex-team.ru/arcadia/taxi/backend-py3/services/eslogadminpy3/docs/yaml/filters_schema.yaml), индексируемые tariff-editor'ом

## Поля объекта `req`, используемые `tariffEditorResolver`

### Структура:

-   `имя_свойства_req`/`имя_свойства_логгера` - `имя_свойства_в_tariff_editor`: описание свойства

### Ожидаемые поля в объекте `req`:

-   `method` - `method`

-   `totalTimings` - `delay`: время (в ms), за которое был обработан запрос.
-   `requestId` - `link`: идентификатор запроса, состоящий из шестнадцатеричных символов. невзирая на то, что при отсутствии `requestId` будет сгенерирован _nanoid_ длины 32.
-   `url` - `url`: по умолчанию - ручка, в которую был сделан запрос
-   `metaType` - `meta_type`: поле ‘type’, отображаемое в tariff-editor; по умолчанию - _pathname_ ручки `url`; если не определен `url` - по умолчанию `req.path`

### Опциональные поля в объекте `req`

-   `headers['user-agent']` - `useragent`
-   `headers['x-yataxi-userid']` - `meta_user_id`
-   `headers['x-yandex-uid']` - `meta_user_uid`

## Ремаппинг полей

При вызове функции `tariffEditorResolver` в качестве параметра можно передать объект типа `TariffEditorFields` - в типа этого объекта _не все поля_, которые есть в tariff-editor, но доступен ремаппинг всех основных полей, которые отображаются в админке.

Пример ремаппинга полей при логировании:

```ts
import {TariffEditorFields} from '@lavka-js-toolbox';

const resolver = [
    tariffEditorResolver({
        [TaxiTariffEditorFields.ORDER_ID]: 'myCustomReqidField',
        [TaxiTariffEditorFields.TYPE]: ['my', 'custom', 'nested', 'statusCode', 'field'],
        [TaxiTariffEditorFields.STATUS_CODE]: ['my', 'anotherStatusCode'],
        [TaxiTariffEditorFields.USER_AGENT]: ['not', 'existing', 'path']
    }),
    ...otherResolvers
];

/* инициализируем логгер, передав туда resolver
...
*/

logger.info('AAGAA', {
    req: {
        ...req,
        statusCode: 300,
        myCustomReqidField: 'hello',
        my: {
            anotherStatusCode: 403,
            custom: {
                nested: {
                    statusCode: {
                        field: 'world'
                    }
                }
            }
        }
    }
});
```

При отсутствии ремаппинга, результат вызова метода `info` из предыдущего примера был бы эквивалентен следующему вызову:

```ts
logger.info('AAGAA', {
    req: {
        ...req,
        statusCode: 403,
        orderId: 'hello',
        metaType: 'world'
    }
});
```
