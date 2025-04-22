# Композитный способ оплаты

Обновление протокола относительно предыдущей проработки.


### Protocol

#### paymentmethods

Чтобы клиенты могли отличать в интерфейсе основные способы оплаты от второстепенных (которые используются для композитной оплаты), необходимо добавить дополнительный флаг: **is_complement** и объект с арибутами **complement_attributes**.

Почему в **complement_attributes** типы, а не конкретные методы:
 * Непонятно, зачем нам фильтровать еще и по конкретным методам. Вряд ли мы захотим разрешать по одной карте ехать композитом, а по 
 другой - нет
 * Пункты "applepay" и "googlepay" нормально выглядят среди множества типов, но как-то стремного среди множества конкретных методов
 * По типам можно просто забрать из конфига, а по методам придется еще какую-то логику пилить. И так как в ордеркоммите мы тоже должны проверить сочетаемость, то нам придется или запоминать, какие методы мы разрешили или дублировать проверку

Клиент определяет, композитный метод оплаты это или полноценный только на основании этих полей, никаких клиентских экспериментов.

Эти поля должны быть поддержаны в available-accounts в сервисе taxi-personal-wallet и прокинуты через api-proxy

Флоу работы paymentmethods
* Api-proxy идет за кошельком в available-accounts
* available-accounts проверяет эксперимент complement_personal_wallet_payment
* Добавляет в ответ **is_complement**
* Добавляет в ответ **complement_attributes** с:
    * **name** - название метода оплаты для окна списка оплат.
    * **compatibility_description** - строка с описанием совметимых основых методов оплаты
    * **payment_types** - список совместимых основных методов оплаты
* **compatibility_description** должен зависеть от приложения. Для iOS писать вроде с "Работает с картой или ApplePay", для Android - "Работает с картой или GooglePay"

Про экспермент **complement_personal_wallet_payment**:
* Композит включать по зонам необязательно, по юзерам норм. Для АБ Геша сделает явный список phone_id, потом будет обычное управление по процентам.
* Эксперимент по юзерам, то есть в кварги отдаем phone_id и uid.


Еще делаем конфиг вида: 
```json
COMPLEMENT_TYPES_COMPATIBILITY_MAPPING
{
    "personal_wallet": ["card", "applepay", "googlepay"]
}
```
Массив **complement_attributes.payment_types** должен определяться на его основе

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
        "is_complement": true,
        "complement_attributes": {
          "name": "Плюс - потратить на поездку",
          "compatibility_description": "Работает с картой или ApplePay",
          "payment_types": [
            "card",
            "applepay",
            "googlepay"
          ]
        },
        "is_new": false,
        "money_left_as_decimal": "570",
        "money_left_as_str": "570 $SIGN$$CURRENCY$",
        "name": "Плюс",
        "payment_available": true,
        "payment_orders": [
        ]
      }
    ]
  }
...
```

#### routestats

Планируется дополнить запрос в routestats дополнительным полем complements, который будет содержать массив второстепенных способов оплаты 

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

Флоу работы роутстатс
* Пользователь делает запрос в routestats
* Проверяем эксперимент **complement_personal_wallet_payment**(переименование относительно первой проработки)
* Проверяем сочетание основного метода оплаты и кошелька конфигом COMPLEMENT_TYPES_COMPATIBILITY_MAPPING, <del>отдельным кейсом проверяем нал для показа брэндинга.</del>
* Мы идем в сервис personal_wallet за всеми кошельками юзера
* Отбираем только кошельки по нужной валюте
* Если есть поле complement_payment_methods, то берем id кошелька из него, иначе выбираем максимальный
* Отфильтровываем классы, для которых из них недоступна оплата кошельком.
* Для оставшихся берем баланс выбранного кошелька и формируем брендинги типа **complement_payment**
* И подменяем price на ту часть, что будет оплачена картой/токеном, в original_price пишем полную цену
* Предполагается, что клиент сам разберется, показывать брендинг включенным или нет

Пост MVP
* Если клиент пришел с композитной оплатой, то есть с complement_payment_methods, то для классов, не поддерживающих кошелек, возвращаем tariff_unavailable

```json
{
...
"service_levels": [
    {
        "brandings": [
          {
            "type": "complement_payment",
            "title": "Поехать дешевле",
            "subtitle": "Оплатить часть поездки Плюсом -- 121 $SIGN$$CURRENCY$",
            "payment":
                {
                    "payment_method_id": "wallet_id/1234567",
                    "type": "personal_wallet"
                }
          }
        ]
    }
],
...
}
```

#### orderdraft

Планируется дополнить запрос в orderdraft аналогичным полем как и в routestats. В оффере будет лежать аналогичная структура

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

* Проверяем эксперимент complement_personal_wallet_payment
* Проверяем совместимость основного и второстепенного методов оплаты
* Проверяем, доступна ли для этого класса оплата кошельком

Любая проверка не проходит - 406 и COMPOSITE_PAYMENT_UNAVAILABLE

* На лимит из конфига не проверяем, так как юзер может включить композит в настройках
* Наличия оффера также не требуем, так как в выбранной схеме форсить точку Б смысла нет, а без нее оффера не будет 

И отдельно:
* Если каким-то образом пришел заказ по кошельку как самостоятельному методу оплаты - проверяем эксперимент complement_personal_wallet_payment и если он включен, то не даем создать заказ

Ответ 406:

```json
{
  "error": {
    "code": "COMPOSITE_PAYMENT_UNAVAILABLE",
    "text": "Композитная оплата недоступна"
  }
}
```
