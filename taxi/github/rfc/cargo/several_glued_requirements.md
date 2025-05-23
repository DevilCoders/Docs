## Задача
Для выбора размера машин в грузовом тарифе, хочется, чтобы на карточке тарифа была возможность выбрать одновременно и размер машины, и количество грузчиков.

Сейчас, у требования можно указать признак glued, это значит что требование обязательно для данного тарифа и должно отображаться на саммари. Однако при этом там нельзя вывести 2 требования (по факту будет выведено одно из glued требований).

Также, glued требования считаются обязательными, однако это не очень правильно и хочется иметь возможность управлять этим отдельно. 

И надо иметь возможность заменять картинки в карточке тарифа на указанные в админке.

Справочно дизайн есть в тикете [TAXIPROJECTS-972](https://st.yandex-team.ru/TAXIPROJECTS-972)

## Доработки
### Несколько glued требований
- [2d] на бекэнде для старых клиентов (по третьим экспериментам) надо отправлять только одно требование glued. Будем сортировать по позиции (в админке уже есть поле), и отправлять первое glued, остальные отсекать.
- [?d] поддержать на клиентах несколько glued требований
- [?d] отдельно проверить на клиентах, что дефолтное требование учитывается (сейчас есть сомнения)

### Обязательность требований
- [?d] добавить в админке на экран "Требования" флаг "Данное требование будет опциональным, даже если оно Приклеено". Оно должно сохраняться в коллекцию dbtaxi.requirements и, таким образом, будет распространяться на все тарифы, где используется.
- [2d] добавить в API в ответ `/zoneinfo` поле `optional_glued`:
```json
{
    "max_tariffs": [
        {
            "supported_requirements": [
                {
                "required": false,          // Существующее поле (для Комбо, сейчас используется только в требовании `capacity`), не меняем его логику. Причины почему его не переиспользуем:
                                            // 1. Возможно, оно потребуется если захотят воскрешать Комбо
                                            // 2. Пришлось бы делать разную логику в зависимости от версии клиентов
                "optional_glued": true,     // Новое поле, если оно есть и в значении true, то требование не обязательно, даже если оно glued
                "glued": true,              // Существующее поле
                ...
                "select": {                 // существующие поля, в том числе, для картинок 
                    ...
                    "options": [
                        {
                            "icon": {
                                "size_hint": 206,
                                "url": "https://tc.mobile.yandex.net/static/images/38292/2fd972dc-c50c-4646-a768-afe8e15680ea",
                                "url_parts": {
                                        "key": "TC",
                                        "path": "/static/images/38292/2fd972dc-c50c-4646-a768-afe8e15680ea"
                                }
                            },
                            "image": {
                                "size_hint": 206,
                                "url": "https://tc.mobile.yandex.net/static/images/10593/a5ee8c84-c45b-4b3b-8d86-41fbe45255c8",     // Тут будут приходить картинки для карточки тарифа
                                "url_parts": {
                                    "key": "TC",
                                    "path": "/static/images/10593/a5ee8c84-c45b-4b3b-8d86-41fbe45255c8"
                                }
                            },
                            ...
                        }
                    ]
                }
            ]
        }
    ]
}
```
- [?d] поддержать на клиентах поле `optional_glued` и не делать такие требования обязательными, даже если они `glued`

### Картинки
- картинки уже должны передаваться в `zoneinfo.max_tariffs.supported_requirements.select.options`, надо проверить что на клиенте оно используется и не захардкожено
- [1d] починить баг по которому нельзя загружать в админку фотки с точками в названии: https://st.yandex-team.ru/TAXIBACKEND-25095
