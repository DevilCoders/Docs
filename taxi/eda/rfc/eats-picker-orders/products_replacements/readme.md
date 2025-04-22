## Тикет
https://st.yandex-team.ru/RETAILSPECS-107

## Цель
Надо сохранять информацию о предпочтительном способе коммуникации, и о дефолтном варианте работы с заменами, чтобы пикерка (и, возможно, не только она) могла дальше это использовать.

## Где хранить информацию о политиках
### Вариант 1. В заказе в коре
Не хочется дорабатывать кору, и добавлять лишние данные в заказ.

### Вариант 2. В eats-picker-orders
Используем ручку `POST /api/v1/order/picking-policy` из https://st.yandex-team.ru/RETAILDEV-1333 сохранения данных по заказу в сервис `eats-picker-orders`, который и будет эту информацию потом использовать.

### Вариант 3. В отдельном сервисе
Кажется, слишком мелко для отдельного сервиса.

### Выбираем вариант 2

## Флоу
- на чекауте в ручках ((https://tariff-editor.taxi.yandex-team.ru/control-api-proxy/endpoints/show/Z28tY2hlY2tvdXQ%3D?cluster=api-proxy&search=go-checkout go-checkout)) и в ((https://tariff-editor.taxi.yandex-team.ru/control-api-proxy/endpoints/show/cGEtZ28tY2hlY2tvdXQ%3D?cluster=api-proxy&search=go-checkout pa-go-checkout)) надо будет отдавать, в корне:

```json
{
    // ...,
    "retailReplacements": {
        "communicationPoliciesBlockName": "Что делать при заменах?",
        "communicationPolicies": [
            {
                "id": "by_phone",       // id для передачи на бек
                "name": "По телефону",  // Локализованное название
                "selected": true        // предвыбранный вариант?
            },
            {
                "id": "in_app",
                "name": "В приложении"
            }
        ],
        "notFoundPoliciesBlockName": "Если не отвечаете?",
        "notFoundPolicies": [
            {
                "id": "propose_replacement",
                "name": "Предлагать замену",
                "selected": true
            },
            {
                "id": "skip_item",
                "name": "Не заменять"
            }
        ]
    }
}
```
"selected" будет приходить всегда и для одного значения, но если не так (баг на беке) - предвыбираем по дефолту первое.

Для начала будем брать из эксперимента на бекэнде (так как больше неоткуда).

- фронт отображает их в интерфейсе, юзер их выбирает, и делает заказ

- при формировании заказа в ручку коры `POST /api/v1/orders` передавать, в ((https://github.yandex-team.ru/taxi/schemas/pull/24509/files#diff-12563455fb095341092f56b732d0d76ab4749ca6561e27d762801b3effedd368R11 `extended_options`):
```json
{
    // ...,
    "extended_options": [
        // ...,
        {
            "type": "retail_replacements",
            "communication_policy": "by_phone",
            "not_found_item_policy": "propose_replacement"
        }
    ]
}
```

- в коре, в ручке `POST /api/v1/order` сохранять эти новые extended_options в БД сервиса

- в коре, при отправке данных в ProcaaS, отправлять при создании заказа метаданные в payload события

- при получении события `created`, ходить в ручку `eats-picker-orders` для сохранения их в этом сервисе
