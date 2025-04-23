# Композитный способ оплаты

Композитный способ оплаты предполаагет возможность оплатить поездку частично картой, частично кошельком. Для MVP предполагается, что мы снимаем все деньги с кошелька, а остаток по заказу оплачивается картой. 


## Утвержденный флоу

### Discounts

Так как скидки могут быть привязанны к конкретному способу оплаты, то в рамках MVP
 было решено не использовать скидки при использовании композитного способа оплаты. Для этого надо поменять api
  ручки calculate-discounts, добавив туда поле complement_payment_methods
   и в ответе всегда возвращать пустой массив скидок
  
 ```json
{
...
"payment_type": "card",
"complement_payment_methods": [
    {
        "type": "personal_wallet"
    }
],
...
}
```


### db.orders

Хранить дополнительные способы оплаты планируется в коллекции db.orders

```json
{
    "payment_tech": {
        "type": "card",
        "main_card_payment_method_id": "card-x501fecae85e6eb251f1078e8",
        "complements": [
            {
                "type": "personal_wallet",
                "payment_method_id": "wallet_id/1234567"
            }
        ]
    }
}
```


### processing

Правки в функции синхронизации прока и ордера, надо синхронизировать новый поля payment_tech в order_proc

### change_payment

~~При смене способа оплаты на этот же способ оплаты оставлять композитный способ оплаты, иначе сбрасывать.~~ 

Биллинг обещал поддержать все способы оплаты (card, apple pay, google pay), поэтому надо только учесть сброс на нал.
 при сбросе на наличку надо убирать кошелек из композитных способов оплаты (надо только массив complements делать пустым).

### /v1/internal/payment/split
 
Ручка разделения стоимости поездки по способам оплаты из сервиса кешбека

Request:

```json
{
    "sum_to_pay": {
        "ride": "100",
        "tips": "100"
    },
    "payment": {
        "type": "card",
        "method_id": "card_payment_method",
        "complements": [
            {
                "type": "personal_wallet",
                "payment_method_id": "wallet_id/1234567"
            }
        ]
    },
    "currency": "RUB",
    "brand": "yataxi",
    "order_status": "completed",
    "fixed_price": true
}
```

Response:

```json
{
    "sum_to_pay": {
        "ride": [
            {
                "type": "card",
                "payment_method_id": "payment_card_id",
                "sum": "30"
            },
            {
                "type": "personal_wallet",
                "payment_method_id": "wallet_id/1234567",
                "sum": "70"
            }
        ],
        "tips": [
            {
                "type": "card",
                "payment_method_id": "payment_card_id",
                "sum": "100"
            }
        ]
    },
    "currency": "RUB"
}
```

на этапе MVP разделятся будут только платежи типа ride, все остальные типы платежей будут сниматься с основного способа оплаты

Что творится внутри:
* Если заказ в статусе completed
, то разбивка производится в соотношении, что снимается текущая сумма с кошелька, а остаток с основного
* Если заказ в статусе transporting и fixed_price = true, то алгоритм разбивки аналогичен предыдущему пункту
* Если заказ в статусе transporting и fixed_price = false, то вся сумма заказа снимается с основного способа оплаты
* Если заказ canceled, то все снимается с основного способа оплаты


### Монитиринги, графики, дашборды

#### Мониторинги

Для отслеживание состояния фичи будет достаточно текущих мониторингов на stq
-fails (processing, update_transactions) и vhost-500 (taxi_api, cashback)


#### Продуктовые графики

Кажется, что будет достаточно текущих графиков personal_wallet 

График заказов со смешанным способом оплаты при необходимости можно будет построить в кибане не отправляя метрику в соломон, а статистику по заказам можно вытаскивать при помощи запросов в yt


## Часть для ознакомления

### Clients
На клиентской стороне показом формата флоу будет управляться экспериментом 3.0 complement_payment

![](https://jing.yandex-team.ru/files/shchesnyak/Screenshot%20from%202020-01-29%2017-19-39.png)

### Protocol (Не финальная версия, только для ознакомления)

#### paymentmethods

Чтобы клиенты могли отличать в интерфейсе основные способы оплаты от второстепенных (которые используются для композитной оплаты), необходимо добавить дополнительный флаг: **complement_payment_method**

Этот флаг должен быть поддержан в available-accounts в сервисе taxi-personal-wallet и прокинут через api-proxy


Пример ответа paymentmethods:
```json
...
  "personal_wallet": {
    "available_accounts": [
      {
        "currency_rules": {
          "code": "RUB",
          "sign": "₽",
          "template": "$VALUE$ $SIGN$$CURRENCY$",
          "text": "rub"
        },
        "deposit_available": false,
        "deposit_payment_methods": [
        ],
        "discounts": [
        ],
        "id": "wallet_id/4020053542",
        "can_be_complement": true,
        "is_new": false,
        "money_left_as_decimal": "570",
        "money_left_as_str": "570 $SIGN$$CURRENCY$",
        "name": "Plus",
        "payment_available": true,
        "payment_orders": [
        ]
      }
    ]
  }
...
```

#### routestats

Планируется дополнить запрос в routestats дополнительным полем complement_payment_methods
. Который будет содержать массив второстепенных способов оплаты 

```json
{
...
"payment": {
    "payment_method_id": "card-xbc2a4abe74f27f186d76ef99",
    "type": "card",
    "complements": [
        {
            "type": "personal_wallet",
            "payment_method_id": "wallet_id/1234567"
        }
    ]
},
...
}
```

Флоу работы роутстатс, когда не включено использование кошелька:
* Пользователь делает запрос в routestats без поля complement_payment_methods
* Внутри плагина происходит проверка доступности кошелька, поход в сервис кошелька за балансом и возврат брендинга 

```json
{
...
"service_levels": [
    {
        "brandings": [
          {
            "type": "complement_personal_wallet_payment_popup",
            "title": "Оплатить часть поездки Плюсом -- 121 $SIGN$$CURRENCY$",
            "payment_method_id": "wallet_id/12345678"
          }
        ]
    }
],
...
}
```

когда пользователь переключает "тумблер", то делается перезапрос в routestats
 с полем complements
. Плагин все так же идет за балансом и возвращает дополнительный брендинг с новой ценой

```json
{
...
"service_levels": [
    {
      "brandings": [
        {
          "type": "complement_personal_wallet_payment_popup",
          "title": "Оплатить часть поездки Плюсом -- 121 $SIGN$$CURRENCY$",
          "value": "enabled",
          "payment_method_id": "wallet_id/12345678"
        }
      ]
    }
],
...
}
```

#### orderdraft

Планируется дополнить запрос в orderdraft аналогичным полем как и в routestats
. В офере будет лежать аналогичная структура

```json
{
...
"payment": {
    "payment_method_id": "card-xbc2a4abe74f27f186d76ef99",
    "type": "card",
    "complements": [
        {
            "type": "personal_wallet",
            "payment_method_id": "wallet_id/1234567"
        }
    ]
},
...
}
```

#### ordercommit

При поиске оффера нужно матчить еще и по композитам
Мы все еще можем не найти оффер, даже если клиент дождался ответа routestats
 и юзер все видел и принял – поэтому если пришел композит и оффера нет - 406
 , с кодом COMPOSITE_PAYMENT_UNAVAILABLE
Кажется, даже плагин не нужен. Просто еще одна проверка в commit_state_handling в HandlePending

Пример ответа 406:

```json
{
  "error": {
    "code": "COMPOSITE_PAYMENT_UNAVAILABLE",
    "text": "Композитная оплата недоступна"
  }
}
```

### update_transactions (этой чатстью будет заниматься биллинг, оставил для ознакомления)

![](https://wf.yandex-team.ru/plantuml/jLF1IiGm4BtFLmmvAwso8FGW-n4Uz5HY6jXWDWr9jek880fwz5T4HSlAwYyaVsIwkprqQQ4U92HXNjwRnsIOgNNKkCLSWcLKSZn9KroAmiq0GCSNmOIcoY5Pw88wdZj3bQNCYL9PWjHY3zuLdkqhXgcCsjabPLSRMXi0z5ZWuMadJuQ9K5Kf64yCTqRmYiC-loTDXfDqybS3PdXa5-Fo7wTfXZlbe55RQZIfZgAFuqPHcLWjXSirlPvpvQ0b3LhT4CsDBQCoNr8fkICPadDoqFohAPhWWjoEBBQjTKiUNIg0B4kD_YSy-A-uQh_sR-XVqN_xZnYz-vU8rBvkW5NSw_2qXS8pXljmjma-uxaAZmtlNtlVwSs0KPyGk2hYUC0qtitam2y0)

В рамках перехода на композитный способ оплаты предполагается ходить в сервис transactions, вместо траста, флоу при этом остается почти таким же:

* Если выбран композитный способ оплаты, то необходимо получить инвойс через ручку /invoice/retrieve
, если инвойс не нашелся, то создать /invoice/create,
 проверить статус текущих платежей и если транзакция находится не в терминальном статусе (HOLD_SUCCESS, HOLD_FAILED
 , CLEAR_SUCCESS
 , ...)
 , то перепланировать update_transactions
* Если все транзакции завершены, то через ручку /v1/internal/split_payment
 необходимо получить разбивку цены по способам оплаты 
 * Инициировать транзакцию через ручку /invoice/update
  передав туда сумму к списанию как с кошелька, так и с карты\google pay
  \apple pay и перепланировать update_transactions на более поздний период
 
 Необходимо правильно обрабатывать ошибки от сервиса транзакций и выбрасывать сооветсвующие исключения, которые случаются при походе в траст
 
 остальной флоу остается старым
