## Где мы взаимодействуем с клиентом

1. Загрузка приложения. Ручки `/3.0/paymentmethods` или `/3.0/cards` (для старых клиентов)
2. Нажатие кнопки "Заказать". Ручки `/3.0/ordercommit` или `/3.0/order` (для старых клиентов)
3. Экран оплаты заказа в Лавке/Еде. Ручка `/4.0/payments/v1/list-payment-methods`
4. Смена способа оплаты. Ручка `/3.0/changepayment`


## Ручка `/3.0/paymentmethods`

Сейчас ответ ручки `/3.0/paymentmethods` выглядит следующим образом:

```json
{
    "merchant_id_list": [...],
    "last_payment_method": {...},
    "personal_wallet": {...},
    "card": {
        "payment_available": true,
        "available_cards": [
            {
                "number": "****9534",
                "busy": false,
                "expiration_time": "2022-02-28T00:00:00+0000",
                "system": "MasterCard",
                "expiration_month": 5,
                "expiration_year": 2021,
                "currency": "RUB",
                "id": "card-x5678",
                "usable": true
            },
            {...},
        ],
        "unverified_cards": [
            {
                "number": "****9534",
                "busy": false,
                "expiration_time": "2022-02-28T00:00:00+0000",
                "system": "MasterCard",
                "expiration_month": 5,
                "expiration_year": 2021,
                "currency": "RUB",
                "id": "card-x5678"
            },
            {...}
        ]
    },
    "corp": {...},
    "coop_account": {...}
}
```

Поле `card.available_cards.usable` сейчас всегда заполняется `true`. Так оно и останется.
Клиенты это поле парсят и у них на него есть тесты, но ни в какой логике это поле не участвует.

Все карты, которые заблочены **card-antifraud**, будут попадать в `unverified_cards` и не будут
попадать в `available_cards`. К ним будет добавляться дополнительное поле `verify_strategy` со значением `card_antifraud` в случае блокировки `card-antifraud`.


## Ручка `/3.0/cards`

Сейчас ответ ручки выглядит следующим образом:

```json
{
    "available_cards": [
        {
            "busy": false,
            "currency": "RUB",
            "expiration_month": 5,
            "expiration_time": "2022-05-31T00:00:00+0000",
            "expiration_year": 2022,
            "id": "card-x73ce075cfc2118a9bb2fab23",
            "number": "****9242",
            "system": "VISA",
            "usable": true
        },
        {
            "busy": false,
            "currency": "RUB",
            "expiration_month": 5,
            "expiration_time": "2022-05-31T00:00:00+0000",
            "expiration_year": 2022,
            "id": "card-x2a206d8eceffd3e52bccabb9",
            "number": "****4867",
            "system": "VISA",
            "usable": true
        }
    ],
    "payment_available": true
}
```

В отличие от `/3.0/paymentmethods` здесь нет поля **unverified_cards**, поэтому ответ тут на самом деле другой.

Так как это legacy ручка, сделать здесь просто фильтрацию по антифроду без возможности сообщить клиенту, как обрабатывать ситуацию.
Оно ведь так сейчас и сделано.

Поэтому, в случае блокировки карты антифродом, будет просто такой ответ:

```json
{
    "available_cards": [],
    "payment_available": true
}
```

## Ручки `/3.0/ordercommit` или `/3.0/order`

Ручка `/3.0/orderdraft` остается без изменений.

В ручки `/3.0/ordercommit` и `/3.0/order` добавляется новый код ошибки - `NEED_CARD_ANTIFRAUD`.

То есть, в случае ошибки ответ ручки будет такой:

```json
HTTP/1.1 406 Not Acceptable
{
    "error": {
        "code": "NEED_CARD_ANTIFRAUD",
        "text": "Какой-то текст из танкера"
    }
}
```


## Ручка `/4.0/payments/v1/list-payment-methods`

Сейчас ответ ручки `/4.0/payments/v1/list-payment-methods` выглядит следующим образом:

```json
{
    "merchant_id_list": [...],
    "last_used_payment_method": {...},
    "payment_methods": [
        {
            "number": "123123****4565",
            "title": "MasterCard",
            "system": "MasterCard",
            "type": "card",
            "currency": "RUB",
            "available": true,
            "id": "card-x1234",
            "bin": "123123"
        },
        {
            "type": "corp",
            "name": "Yandex Badge",
            "id": "badge:yandex_badge:RUB",
            "description": "оплата бейджиком",
            "currency": "RUB",
            "availability": {
                "available": true,
                "disabled_reason": ""
            }
        },
        {...}
    ]
}
```

Сейчас у разных способов оплаты есть разные поля, сигнализирующие, достепен способ оплаты или нет. У карт есть поле `available`, которое формируется на основе поля `valid`, получаемого из Траста. У корпов есть структура `availability` с двумя полями
`{"available": true, "disabled_reason": ""}`.

Старые клиенты поддерживают только поле `available`.
Новые клиенты поддерживают структуру `availability` (для всех типов оплаты) и фолбечатся на поле `available`, если нет `availability`.

Причем, если в структуре `availability` поле `disabled_reason` отсутствует (имеет пустое значение или NULL), то клиент сам выводит текст из
[танкерного ключа](https://tanker.yandex-team.ru/?project=taxi&branch=master&keyset=TAXIA.Strings&key=payment_verify).

То есть, мы должны что-либо посылать в поле `disabled_reason` только, если хотим написать свой текст.

Договорились на встрече 27 февраля, что верификации в супераппе не будет, то есть значение поля `disabled_reason` в ручке `/4.0/payments/v1/list-payment-methods` сейчас не имеет значения. Пусть клиент пишет значение, которое он получает из танкера.

В дальнейшем, если мы захотим какой-то флоу верификации, то на клиенте нужно будет сделать обработку `disabled_reason`. То есть воспринимать её ни как сообщение для пользователя, а как машиночитаемый код. Или добавить какое другое поле.

В итоге ответ для карт будет таким:

```json
{
    "merchant_id_list": [...],
    "last_used_payment_method": {...},
    "payment_methods": [
        {
            "number": "123123****4565",
            "title": "MasterCard",
            "system": "MasterCard",
            "type": "card",
            "currency": "RUB",
            "available": true,
            "availability": {
                "available": true,
                "disabled_reason": ""
            }
            "id": "card-x1234",
            "bin": "123123",
        },
        {...}
    ]
}
```

Такая же структура с методами оплаты возвращается в ответе ручки `/4.0/payments/v1/preorder` ключ `payment_methods`. Эта ручка используется, когда пользователь нажимает на кнопку "Заказать" в супераппе.
Тут структура должна совпадать с `list-payment-methods`. Так и будет.

## Ручка `/3.0/changepayment`

В случае невозможности сменить способ оплаты из-за `card-antifraud` будет такой ответ:

```json
HTTP/1.1 406 Not Acceptable
{
    "error": {
        "text": "need_card_antifraud",
    }
}
```

Такой формат у всех ошибок ручки `/3.0/changepayment`. Делаю так для консистентности.
