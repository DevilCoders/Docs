# Продвижение подписки v2

## Проблема

Нужно добавить информацию о подписке v2 в брендинги, пуши, 
в карточку заказа и продумать как расскатить кешбек 
на всех пользователей в totw.

## Анализ

### Брендинги (Продвижение подписки на саммари)

#### Старый брендинг скидочной подписки (`plus_promotion`):

<img src="https://jing.yandex-team.ru/files/arteeemik/summary.jpg" alt="summary" width="200" height="400">

Брендинги формируются в routestats. 
Код:
- `MakePlusPromotionBranding()` ([код](https://github.yandex-team.ru/taxi/backend-cpp/blob/ed0d758e75935194e6c28d143b859c16b419b4d2/protocol/lib/src/views/routestats/brandings/builders.cpp#L225))
  - ключ `routestats.brandings.plus_promo.title`
 
Выключаем эксперимент [plus_promotion](https://tariff-editor.taxi.yandex-team.ru/experiments3/show/plus_promotion?type=experiments&name=plus_promotion)
в тех странах, где будет работать кэшбэчная подписка, чтобы не показывать брендинг про скидочную подписку там.

  
#### Нужно реализовать новый брендинг (`plus_v2_promotion`):

<img src="https://jing.yandex-team.ru/files/arteeemik/summary_v2.jpg" alt="summary" width="200" height="400">

Предполагается написать новую функцию:
- `MakePlusV2PromotionBranding()` с таким ответом в routestats (новый тип: `plus_v2_promotion`):
```json
{
    "brandings": [
        {
            "title": "Поехать на 870 рублей дешевле",
            "subtitle": "Активируйте баллы в Плюсе",
            "type": "plus_v2_promotion"
        }
    ]
}
```
Нужно в этой функции формировать брендинг, если выполняются следующие условия:
- у пользователя нет подписки (нужно проверить, что флаг 
`has_ya_plus == False`, он приходит из хедеров со стороны PA)
- есть баллы на кошельке (Для проверки баланса кошелька 
можно воспользоваться функцией `RoutestatsData.GetPersonalWalletBalance()`)
- формировать новый брендинг, если смачился эксперимент `plus_promotion_v2` (новый эксперимент, 
который будет активен в той стране, где активна кэшбэчная подписка)

Код предполагается писать в routestats, который будет в uservices: 
[TAXIBACKEND-29176](https://st.yandex-team.ru/TAXIBACKEND-29176)
 (ориентировочно сам сервис поедет в прод на этой неделе, 
 а код в новом routestats можно будет начать писать со следующей недели)


#### Также необходимо реализовать новый брендинг (`plus_cashback_promotion`):

<img src="https://jing.yandex-team.ru/files/arteeemik/cashback_summary.jpg" alt="summary" width="200" height="400">

Предполгается написать новую функцию: 
- `MakePromotionCashbackBranding()` с таким ответом в routestats:
```json
{
    "brandings": [
        {
            "title": "Кэшбэк 120 баллов, если подключить подписку Яндекс.Плюс",
            "type": "plus_cashback_promotion"
        }
    ]
}
```
Нужно формировать брендинг только, если выполняются следующие условия:
- у пользователя нет подписки (нужно проверить, что флаг `has_ya_plus == False`)
- за данный класс может быть начислено много кэшбэка
- активен эксперимент `cashback_for_plus` в этой стране, 
то есть кэшбэчная подписка работает в стране пользователя

Предполгается завести новый конфиг: PLUS_CASHBACK_PROMOTION_SETTING
в котором будет разбивка по странам с минимальным кэшбэком, начиная с которого будем формировать этот брендинг.

Пример, как будет выглядеть конфиг: 
```json
{
  "fi": 
     {
        "min_cashback": 100
     },
  "ru": 
    {
        "min_cashback": 100
    }
}
```

Вычислять кэшбэк нужно аналогично этой функции: [MakeCashbackBranding](https://github.yandex-team.ru/taxi/backend-cpp/blob/develop/protocol/lib/src/views/routestats/brandings/builders.cpp#L224)
В этой функции недавно добавили вычисление готового значения кэшбэка в этом тикете: https://st.yandex-team.ru/TAXIBACKEND-29344


### Пуш про оплату поездки

Нужно добавить информацию о кэшбэке в пуш про оплату поздки, как на примерах ниже:

| ![Summary](https://jing.yandex-team.ru/files/arteeemik/оплата_плюсом.png) | ![Summary](https://jing.yandex-team.ru/files/arteeemik/композитка.png) | ![Summary](https://jing.yandex-team.ru/files/arteeemik/Пуш_плюс_кэшбек.png) |
| -- | -- | -- |

Пуш пользователю с просьбой оценить заказ (пример: "Стоимость 300 руб. Оцените поездку"):
формируется в `stq/processing` в функции `notify_on_complete`: [код](https://github.yandex-team.ru/taxi/backend/blob/develop/taxi/internal/order_kit/plg/status_handling.py#L1065)

Предполагается в этой функции понимать является ли заказ кэшбэчным, 
оплаченым полностью кошельком или в качестве способа оплаты выбрана 
композитная оплата, и в зависимости от этого формировать новый текст пуша.

Эту информацию предполагается узнавать из дока order_proc, 
который передается в эту функцию.


###  Надпись "Без кэшбэка" на карточке заказа

Пример, как это должно выглядеть когда нет кэшбэка / когда есть кэшбэк:

| <img src="https://jing.yandex-team.ru/files/arteeemik/2020-06-25%2022.26.29.jpg" alt="summary" width="200" height="400"> | <img src="https://jing.yandex-team.ru/files/arteeemik/Screen%20Shot%202020-06-30%20at%205.09.43%20PM.png" alt="summary" width="200" height="400"> |
| -- | -- |

Чтобы показывать эту запись, нужно чтобы выполнялись следующие условия:
- нет подписки у пользователя (нужно проверить, что флаг `has_ya_plus == False`)
- Пользователь находится в определенной стране (для этого нужно будет завести новый эксперимент)
- едешь в плюсовых тарифах
- за текущую поездку нет кэшбэка

Информацию в карточке заказа берется из totw. 

Сейчас флоу такой: 
- если из totw в поле `cost_message_details` не приходит поле `cashback`, то показывается надпись: `"Как вам поездка?"`
- если из totw в поле `cost_message_details` приходит поле `cashback`, то показывается надпись: `"Кэшбэк: 20 Р"`

Пример поля `cost_message_details`:

```(json)
{
  "cost_message_details": {
    "cost_breakdown": [],
    "extra_info": [],
    "cashback": {
      "value_as_str": "24 $SIGN$$CURRENCY$"
    }
  }
}
```

Поле `cashback` добавляется к полю `cost_message_details` в api-proxy 
(Тестовая ручка для проверки работоспособности добавления нотификаций о кешбеке в конфиге `api-proxy`: 
[test/taxiontheway](https://tariff-editor.taxi.tst.yandex-team.ru/control-api-proxy/endpoints/show/L3Rlc3QvdGF4aW9udGhld2F5L2Nhc2hiYWNr) )
через сервис cashback, ручку 
`/internal/totw/info`: [doc](https://github.yandex-team.ru/taxi/backend-py3/blob/develop/services/cashback/docs/yaml/api/internal_totw.yaml#L13)

Для того, чтобы добавить надпись "Без кэшбэка" предполагается расширить протокол, и добавить в поле ответа totw
`cost_message_details.cashback` дополнительное поле `subtitle` и `type`:

```(json)
{
  "cost_message_details": {
    "cost_breakdown": [],
    "extra_info": [],
    "cashback": {
// новые поля
       "action": {
            "type": "buy_plus"
        },
       "title": "без кэшбэка"
// конец новых полей
    }
  }
}
```

Также предлагается обновить протокол ответа, когда есть кэшбэк, добавив поле title (был без title,
и клиентам приходилось слово Кэшбэк переводить у себя самим):

```(json)
{
  "cost_message_details": {
    "cost_breakdown": [],
    "extra_info": [],
    "cashback": {
        "value_as_str": "24 $SIGN$$CURRENCY$",
// новое поле
        “title”: “Кэшбэк: ”
// конец нового поля
    }
  }
}
```


Чтобы не нагружать логику в totw, правки предлагается делаться в ручке `/internal/totw/info`.
Изменения в протоколе ручки `/internal/totw/info`:

```diff

+ CashbackAction:
+        type: object
+        additionalProperties: false
+        required:
+            - type
+        properties:
+            type:
+                type: string
+                example: buy_plus

CashbackDetails:
        type: object
        additionalProperties: false
-        required:
-            - value_as_str
        properties:
            value_as_str:
                type: string
                description: Размер кэшбека с валютой.
                example: 24 $SIGN$$CURRENCY$
+            title:
+                type: string
+                example: Кэшбэк: 
+            action:
+                $ref: '#/definitions/CashbackAction'

```


### Сделать возможным раскатку кэшбэка в totw на всех пользователей

Сейчас есть ручка `/internal/totw/info`: [doc](https://github.yandex-team.ru/taxi/backend-py3/blob/develop/services/cashback/docs/yaml/api/internal_totw.yaml#L13)
предполагалось, что она будет дергаться из [api-proxy] totw, но из-за того, что сервис cashback предел стабильного rps одной машинки
находится в районе 800 RPS (эта информация из тикета: [TAXIBACKEND-27959](https://st.yandex-team.ru/TAXIBACKEND-27959))
При условии 2400 (самый худший случай, когда пик достигается и на transporting, и на complete статусах) RPS на transporting + complete статусы со стороны totw. (средний rps - 700) 

При этом ручка `/internal/totw/info` в `api-proxy` подключается через эксперимент
 [protocol_totw_cashback_info](https://tariff-editor.taxi.tst.yandex-team.ru/experiments3/show/protocol_totw_cashback_info?type=experiments&name=protocol_totw_cashback_info)
 его нужно будет по странам фильтровать, где есть кэшбэчная подписка

Есть несколько вариантов:
- Дождаться пока будет сделано кэширование в api-proxy: [TAXIORDER-278](https://st.yandex-team.ru/TAXIORDER-278). 
 Но кажется, что это будет еще не скоро
- Переписать эту ручку на uservices
- Оптимизировать питонячие сервисы
- Добавить новую машинку для сервиса cashback
- Изменить логику ручку, чтобы она вызывалась только на статусе заказа `complete`, тогда
пиковая нагрузка на ручку будет до 600 rps
- Заиспользовать новый поллинг данных в totw (заработает примерно в середине августа, то есть для нас этот вариант не подходит, так как нам нужно до 10-15 июля реализовать фичу)

В итоге было принято решение переписать ручку на uservices, объединив с ручкой /internal/v1/taxiontheway/list
, в которую уже ходит totw, написать новую ручку /internal/v2/taxiontheway/list в сервисе plus



# Разработка

## Скоуп по задачам

* Добавить в пуш про оплату поездки информацию о кошельке (stq/processing) (3d)
* Брендинг "может быть начислено X баллов" (uservices/routestats) (2d)
* Брендинг "поехать дешевле с подпиской" (uservices/routestats) (2d)
* Надпись "Без кэшбэка" на карточке заказа (uservices/plus) (2d)
* Написать новую ручку /internal/v2/taxiontheway/list (uservices/plus) (5d)
* Поддержать ручку /internal/v2/taxiontheway/list  (api-proxy/totw) (3d)
* Добавить кэширование данных(рейтов) в ручке /internal/v2/taxiontheway/list (uservices/plus) (3d)
