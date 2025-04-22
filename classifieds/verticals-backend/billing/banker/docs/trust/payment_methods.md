## Платежные методы

### Способы оплаты в трасте
Способы оплаты в трасте делятся на 2 типа:
* **bound_payment_methods** - привязанные способы оплаты (платежные средства)
* **enabled_payment_methods** - разрешенные способы оплаты

Привязанные способы оплаты используются для оплаты "в один клик" из мобильного приложения и для рекуррентных платежей через api.
На данный момент в качестве привязанных способов оплаты возвращаются банковские карты, но в будущем могут появиться и другие способы, например, баллы Яндекс.Плюса или кошелек в Я.Pay.
Чтобы совершить оплату с помощью привязанного способа оплаты, при создании корзины необходимо указать **payment_mode** = **api_payment** и в качестве **paymethod_id** передать **id** карты, который вернулся из траста.

Пример привязанного способа оплаты:
```
{
    "card_country": "ROU",
    "last_paid_ts": 1644577183.789732,
    "region_id": 225,
    "last_service_paid_ts": 1644577183.789732,
    "payment_method": "card",
    "payment_system": "MasterCard",
    "system": "MasterCard",
    "expiration_month": "04",
    "last_paid": 0,
    "binding_ts": "1644577184.056",
    "ebin_tags_version": 4,
    "card_level": "",
    "holder": "CARD HOLDER",
    "id": "card-x75ab11a2dbdd17dba2e35443",
    "last_service_paid": 0,
    "account": "510000****1253",
    "isoa2": "RO",
    "ebin_tags": [],
    "expiration_year": "2025",
    "aliases": [
        "card-x75ab11a2dbdd17dba2e35443"
    ]
}
```

Разрешенные способы оплаты дают информацию о том, какие платежи поддерживает терминал траста в принципе.
На данный момент имеем разрешенный способ оплаты - с помощью произвольной банковской карты (необязательно привязанной к пользователю).
Поля возвращаемого способа оплаты указывают свойства и ограничения, характерные для него:
* **currency** - ISO код валюты терминала
* **firm_id** - код фирмы по справочнику - юр. лицо Яндекса, которое принимает оплату
* **payment_systems** - платежные системы, поддерживаемые терминалом

Разрешенный способ оплаты не имеет **id**. Чтобы совершить оплату с помощью него, при создании корзины необходимо указать **payment_mode** = **web_payment** и в качестве **paymethod_id** передать **trust_web_page**.
Информация, содержащаяся в разрешенном способе оплаты используется лишь для отображения web-формы на фронтенде в случае, если используется не стандартная, а кастомная форма.

Пример разрешенного способа оплаты:
```
{
    "payment_method": "card",
    "currency": "RUB",
    "firm_id": 12,
    "payment_systems": [
        "MIR",
        "Maestro",
        "MasterCard",
        "VISA",
        "VISA_ELECTRON"
    ]
}
```

### Методы оплаты в банкире
Для получения из API банкира методов оплаты траста необходимо обязательно передавать заголовок **X-Yandex-Uid**, это касается следующих ручек:
* [GET /service/{service}/customer/{customer}/method](http://banker-api-http-api.vrts-slb.test.vertis.yandex.net/swagger/#!/method/allMethods)
* [GET /service/{service}/customer/{customer}/method/gate/{gate}](http://banker-api-http-api.vrts-slb.test.vertis.yandex.net/swagger/#!/method/methodsByPsRoute)
* [GET /service/{service}/customer/{customer}/method/gate/{gate}/method/{method}](http://banker-api-http-api.vrts-slb.test.vertis.yandex.net/swagger/#!/method/methodsByIdRoute)
* [POST /service/{service}/customer/{customer}/payment](http://banker-api-http-api.vrts-slb.test.vertis.yandex.net/swagger/#!/payment/paymentMethodsRoute)

Банкир с целью обратной совместимости с текущими потребителями на уровне API не делает структурных различий между привязанными и разрешенными способами оплаты из траста, отдавая все одним списком.
Различие заключается лишь в наборе возвращаемых полей.

Пример ответа банкира:
```
[
  {
    "editable": false,
    "method": "card-x5cecf7f62ee6d3643f8f3f7c",
    "name": "Привязанная карта",
    "properties": {
      "cardBank": "CITIZENS STATE BANK",
      "cardBrand": "mastercard",
      "cddPanMask": "510000|5432",
      "expireMonth": "11",
      "expireYear": "2022",
      "verificationRequired": false
    },
    "system": "trust"
  },
  {
    "editable": false,
    "method": "card-x02d1fbe61e5937d5552a9c4f",
    "name": "Привязанная карта",
    "properties": {
      "cardBank": "TINKOFF",
      "cardBrand": "mastercard",
      "cddPanMask": "510000|1324",
      "expireMonth": "11",
      "expireYear": "2024",
      "verificationRequired": false
    },
    "system": "trust"
  },
  {
    "editable": false,
    "method": "card",
    "name": "Новая карта",
    "properties": {
      "currency": "RUB",
      "firmId": 12,
      "paymentSystems": [
        "MIR",
        "Maestro",
        "MasterCard",
        "VISA",
        "VISA_ELECTRON"
      ]
    },
    "system": "trust"
  }
]
```
В данном случае у пользователя есть 2 привязанные карты (метод оплаты называется **card-xxx**), и, кроме того, он может оплатить новой картой (метод оплаты называется просто **card**).
В случае совершения рекуррентного платежа с привязанной карты в trust в качестве **paymethod_id** будет отправлен id этой карты.
В случае платежа через WEB-форму в trust в качестве **paymethod_id** всегда передаётся **trust_web_page**.

### Варианты интеграции с банкиром
#### api-платежи (рекурренты)
1. Запросить карточные методы оплаты через ручку [GET /service/{service}/customer/{customer}/method/gate/{gate}/method/{method}](http://banker-api-http-api.vrts-slb.test.vertis.yandex.net/swagger/#!/method/methodsByIdRoute), подставив **card** в качестве значения параметра **method**.
2. Выбрать карту из списка привязанных карт
3. При создании платежа передать в качестве метода оплаты id карты, например, **card-x5cecf7f62ee6d3643f8f3f7c**
4. Платеж будет выполнен без участия пользователя. Статус платежа можно запросить через ручку [GET /service/{service}/customer/{customer}/payment/{gate}/{id}](http://banker-api-http-api.vrts-slb.test.vertis.yandex.net/swagger/#!/payment/getPaymentRoute)

#### web-платежи с использованием стандартной формы оплаты
1. Запросить доступность веб-платажей через ручку [GET /service/{service}/customer/{customer}/method/gate/{gate}/method/{method}](http://banker-api-http-api.vrts-slb.test.vertis.yandex.net/swagger/#!/method/methodsByIdRoute), подставив **card** в качестве значения параметра **method**.
2. При создании платежа передать в качестве метода оплаты **card**
3. Отдать на фронт url формы оплаты, полученный от траста

#### web-платежи с использованием кастомной формы оплаты
1. Запросить все методы оплаты через ручку [GET /service/{service}/customer/{customer}/method](http://banker-api-http-api.vrts-slb.test.vertis.yandex.net/swagger/#!/method/allMethods)
2. Проверить доступность метода **card** в списке возвращенных методов
3. При создании платежа передать в качестве метода оплаты **card**
4. Отдать на фронт:
   * **purchase_token** - токен корзины в трасте, возвращается после создания платежа
   * **currency**, **firmId**, **paymentSystems** - взять из метода оплаты **card**
   * список **id** привязанных карт - взять из списка методов оплаты по маске `card-.*`
