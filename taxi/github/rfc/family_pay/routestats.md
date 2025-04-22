### Изменения в routestats API для оплаты семейной картой

#### Как устроено сейчас
В `3.0/paymentmethods` на клиент приходит признак семейной карты
`/cards/available_cards/family` и description
```
description: "Family account: 1000 of 2500rub."
family:
  is_owner: false
  limit: 250000
  expenses: 150000
  currency: RUB
  frame: month
```

Клиент по наличию `family` отображает карту как семейную.

В routestats/orderdraft выбранный метод оплаты не отличается от обычной карты:
```
  "payment": {
    "payment_method_id": "card-x434db6f255a39636ffdf5c5c",
    "type": "card"
  },
```

Проверка доступности заказа в ordercommit по остатку на карте частично реализована, и потенциальных проблем сделать
остальные проверки тоже нет.
Но продуктово хочется чтобы пользователь видел на саммари что заказ недоступен.

#### Зачем менять?
Эти фичи требуют наличия семейных параметров в routestats:
1. Фильтрация доступности категорий тарифов на саммари (сделать недоступной Доставку)
2. Недоступность заказа если поездка дороже остатка на карте

В запросе routestats признак участника семейного отсутствует, можно их получить
если сходить в cardstorage на всяком запросе routestats
но так не получится, это +1000рпс на cardstorage.
## Решение: поход в cardstorage из плагина routestats по клиентскому признаку `/payment/has_limits: true`
**Трудоемкость на бекенде**: 5d = 3d (ordercommit) + 2d (плагин routestats)

**плюсы**:
* минимальные изменения на клиенте

**костыли и минусы**:
* изменения на клиенте
##### Изменение в 3.0/paymentmethods
Для того, чтобы сделать расширение API более общим и подходящим для других методов оплаты с проверкой лимитов
в api-proxy-critical/3-0-paymentmethods добавляем в `/cards/available_cards` новое поле `has_limits: true`
и отдавать семейную карту участника как
```
family:
  is_owner: false
  expenses: 123400
  limit: 345600
  currency: RUB
  frame: month
description: "Family account: 2222 of 3456rub."
has_limits: true
```

##### На клиенте
Предлагается клиенту добавить в запросе routestats флаг `/payment/has_limits: true` для семейных карт участников
(приходят из paymentmethods c `has_limits: true`)
Наличие поля `has_limits` в запросе rs в общем случае **не гарантируется**, если для карты участника оно отсутствует, то семейные проверки на уровне rs будут пропущены.

##### На беке
По этому признаку в плагине routestats ходим в cardstorage/v1/card за актуальной инфой из кеша cardstorage
__параллельно с запросом routestats-internal__
Полученная `family` структура используется для фильтрации категорий после получения service_levels из протокола.

В ordercommit происходит запрос в cardstorage/v1/card и проверки повторяются. В orderdraft передавать флаг `family/is_owner` не требуется.

Актуальный на момент заказа `family` сохраняется в заказ в ordercommit.

### Предлагаемые изменения и оценка
#### ordercommit (3d)
*  добавляем в [ExtraPaymentInfo](https://github.yandex-team.ru/taxi/backend-cpp/blob/develop/protocol/lib/src/orderkit/commit_state_handling.hpp#L61) `family` из запроса cardstorage
* Проверка возможности заказа по категории и по лимиту [где-то здесь](https://github.yandex-team.ru/taxi/backend-cpp/blob/develop/protocol/lib/src/orderkit/card_reserve.cpp#L233)
* [в commitstate](https://github.yandex-team.ru/taxi/backend-cpp/blob/develop/protocol/lib/src/orderkit/commitstate.cpp#L930) пробрасываем `family` в order_proc
#### плагин routestats (2d)
За основу взять плагин maas

* OnContextBuilt: по флагу `/payment/family/is_owner: false` ходим в cardstorage за `family`
* OnGotProtocolResponse: по ценам и категориям делаем какие-то категории недоступными

### Сложные фичи которые предлагаю убрать из первой версии
#### Актуальность лимитов в routestats
routestats получает лимиты не из Траста, а из кеша cardstorage (а ordercommit из Траста). Это значит, если за время сессии Го с карты спишут деньги или владелец уменьшит лимит, проверки в routestats станут неактуальными, но при заказе все обновится и будет ошибка.
Хуже случай, когда во время сессии владелец увеличил лимит, чтобы участник смог сделать заказ, но routestats ему не даст, пока клиент не дернет paymentmethods: кажется, можно решить пушом с линком на методы оплаты если владелец увеличил лимит.

#### Пуш владельцу если лимит превышен в заказе
Случаи, когда routestats разрешил заказ, а ordercommit -- нет будет мало, потому что проверки идентичные.
И никаких действий с картой не произойдет: зачем беспокоить владельца?
