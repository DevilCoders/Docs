# Получение кошельков из траста

## Как мы получаем кошельки сейчас

Схема получения кошельков
`/3.0/paymentmethods`, `/4.0/payments/v1/list-payment-methods`, `payments-eda` -> `taxi-personal-wallet` -> `billing-wallet`

Схема получения карт:
1) `/3.0/paymentmethods`, `/4.0/payments/v1/list-payment-methods`, `payments-eda` -> `cardstorage` -> `trust`
2) `/3.0/paymentmethods`, `/4.0/payments/v1/list-payment-methods`, `payments-eda` -> `card-filter` -> `cardstorage` -> `trust`

Однако, `trust` при каждом запросе карт так же ходит и в `billing-wallet` за кошельками, поэтому он вынужден держать x2 нагрузку от ручек `/3.0/paymentmethods`, `/4.0/payments/v1/list-payment-methods`, `payments-eda`.

## Решение
Не ходим в `available-accounts` за кошельками, получаем их из траста вместе с картами. Так же продукт начинает ходить за кошельками в траст, что выглядит хорошо :ok_hand:

## Реализация
Если мы перестаём ходить в `available-accounts`, клиенты не должны этого заметить. Поэтому нам нужно:

- Добавлять поля для отображения кошелька на клиентах
- Придумать, что делать с полями для домика Плюса, которые мы для быстрого запуска кошелька передавали в ответе available-accounts
- Куда-то деть z-wallet. 

Нам необходимо прокидывать кошелек в следующих местах:

`cardstorage` - ходит за нас в траст. В нем нужно из ручки `payment_methods` траста доставать не только карты, но и кошельки. 

Судя по [твмным правилам](https://tariff-editor.taxi.yandex-team.ru/services/2/edit/354315/tvm-rules), В него ходит порядка ~20 сервисов. После опроса выяснилось, что ничего не должно сломаться, если добавим дополнительное поле в ответ ручки `v1/payment_methods`. 

Кошелёк в ответе траста:
```json
{
    "account" : "w/30b153cc-8e30-58e2-8d1a-1095bc49b915",
    "payment_system" : null,
    "balance" : "99925.00",
    "id" : "yandex_account-w/30b153cc-8e30-58e2-8d1a-1095bc49b915",
    "cached_until_ts" : 1595417217.9932389,
    "update_ts" : 1595417217.9932389,
    "currency" : "RUB",
    "payment_method" : "yandex_account"
}
``` 

Изменение в api кардстораджа:

```diff
    PaymentMethodsResponse:
        type: object
        additionalProperties: false
        required:
          - available_cards
        properties:
            available_cards:
                type: array
                items:
                    oneOf:
                      - $ref: '#/definitions/PaymentMethodDefault'
                      - $ref: '#/definitions/PaymentMethodLegacy'
            unverified_cards:
                type: array
                items:
                    $ref: '#/definitions/PaymentMethodLegacy'
+           wallets:
+               type: array
+               items:
+                   $ref: '#/definitions/PaymentMethodWallet'

definitions:
+    PaymentMethodWallet:
+        type: object
+        additionalProperties: false
+        required:
+          - wallet_id
+          - balance
+          - currency
+        properties:
+            wallet_id:
+                type: string
+                description: id кошелька
+            balance:
+                type: string
+                description: Баланс кошелька
+            currency:
+                type: string
+                description: Валюта кошелька
+

```
## Идеальный вариант
Кардсторадж вернёт только id, валюту и баланс, для отображения на клиентах мы должны прицепить к кошельку больше полей (далее "обогатить"). В кардфильтре обогащать кошельки - плохая идея, потому что его основная задача - фильтровать способы оплаты, формировать поле `availability`/`available`, и, максимум, отдавать статику. Для кошельков же многие поля имеют нетривиальную логику создания. Идеальным вариантом было бы ходить из клиентских ручек не в `card-filter`, а в сервис, например, `plus-wallet`, который обогатит кошельки данными.
```
                                | cardstorage |
                                |-------------|
                  card-filter - | cards       | 
                /               |             | \
клиентские_ручки                |             |   trust
                \               |             | /
                  plus-wallet - | wallets     | 
                                |             |
```
И на стороне траста сделать фильтрацию по способам оплаты (если ходим за картами, то траст не пойдет в `billing-wallet`). 

**Что не так** - Мы решаем проблему того, что продукт не ходит в траст за кошельками, но перекладываем x2 запросов с `billing-wallet` на `cardstorage` и `trust`, последний, скорее всего, с этим не справится.

Добавление ещё одного слоя прокси для формирования кошельков между клиентскими ручками и кард-фильтром увеличит время получения карт и добавит лишний хоп, что нежелательно. обогащать кошельки в catdstorage нельзя, потому что это продуктовая логика.

**Компромисс** - Не делаем разделение на уровне запросов, делаем разделение на уровне модулей кард-фильтра

```
                   |  card-filter    | 
                   |-----------------|
                   |  cards-module   |
                   |                 |
клиентские_ручки - |                 | - cardstorage - trust
                   |                 |
                   |  wallets-module |
                   |                 |
```
Нужно доставать из кардстораджа, помимо карт, кошельки, обогащать в модуле кошельков, и отдавать их вместе с картами в ручках `/v1/filteredcards/legacy` и `/v1/filteredcards` для `/3.0/paymentmethods` и `/4.0/payments/v1/list-payment-methods`/`payments-eda` соответственно.
В ответе ручек появится куча полей кошелька, изменения в апи смотреть тут -> [card-filter.yaml](./card-filter.yaml) <-

## Клиентские ручки
Ответ `card-filter` нужно прокинуть в клиентские ручки. Изменения в api-proxy:

`/3.0/paymentmethods`:
```diff
      - key: personal_wallet
        enabled#and:
          - value#experiment-effective: personal_wallet
-         - value#source-enabled: personal-wallet-available-accounts
+         - value#if:
+             condition#experiment-effective: wallets_from_trust
+             then#source-enabled: card-filter-filteredcards
+             else#source-enabled: personal-wallet-available-accounts
-       value#source-response-body: personal-wallet-available-accountsss
+       value#object:
+         - key: available_accounts
+           value#get:
+             key: available_accounts
+             object#if:
+               condition#experiment-effective: wallets_from_trust 
+               then#source-response-body: card-filter-filtercards:
+               else#source-response-body: personal-wallet-available-accounts
```

TODO: Прописать протокол для `/4.0/payments/v1/list-payment-methods`
(наброски того как это будет есть в [list-payment-methods.yaml](./list-payment-methods.yaml))

## z-wallets
У каждого пользователя должны быть кошельки, они должны возвращаться в способах оплаты (если ему можно их увидеть). Так как кошелек был экспериментом, мы были ограничены по ресурсам, поэтому создавали их только при пополнении баланса, а отдавали "виртуальные" кошельки (z-wallet). Это не есть хорошо, потому что так продукт занимается созданием кошельков, хотя это задача траста/биллинга. Поэтому в схеме `cardstorage` -> `trust` -> `billing-wallet` нужно либо сразу создавать кошельки, либо отдавать такие же "виртуальные" кошельки

UPD: Обсудили с трастом и биллингом, пришли к общему заключению: виртуальные кошельки - это скорее продуктовая логика, нежели логика биллинга, поэтому z-кошельки будем делать на нашей стороне.

## Формирование полей кошелька
Ручка available-accounts помимо того, что ходила за кошельками, добавляла кучу дополнительных полей в ответ. Их нужно прицепить к каждому из кошельков:

Поле | Где используем | Как оно делается сейчас | Оставляем ли в протоколе | Как будем его делать (*, если так же, как и раньше)
-----|----------------|-------------------------|--------------------------|---------------------
id | На клиентах для создания заказов по кошельку | неизменно отдаётся | + | *
name | Для отображения кошелька в способах оплаты | Разные ключи в танкере в зависимости от: 1) в pass_flags есть флаг cashback_plus 2) Денег на кошельке > 0. | + | *
money_left_as_decimal |используются для отображения баланса в бейдже | balance, придет из траста  | + | *
money_left_as_str | используются для отображения баланса в бейдже | Формируется как f"{balance} $SIGN$$CURRENCY" (balance придет из траста), если нет эксперимента PERSONAL_WALLET_GLYPH, в противном случае просто баланс | + | PERSONAL_WALLET_GLYPH всегда будет включен, потому что у нас всегда будет глиф, поэтому money_left_as_str == balance
currency_rules | Возможно сейчас не используется, но намеренно его не выпиливали | сложно собирается в ручке available-accounts, подробнее в коде https://github.yandex-team.ru/taxi/backend-py3/blob/develop/services/taxi-personal-wallet/taxi_personal_wallet/api/get_available_accounts.py#L455 | +, клиентам не нужно, но оно сейчас используется в payments-eda. На клиентах выпилить, в протоколе оставить | *
payment_available | | есть_плюс and есть_кэшбэчный_плюс(два поля берутся из pass-flags) and матчится эксперимент cashback_for_plus | Отметить как deprecated, на клиентах ходить в availability.| *
deposit_available | ?? | всегда False | deprecated, на клиентах не парсим | *
deposit_payment_methods | ?? | всегда [] | deprecated, на клиентах не парсим | *
payment_orders | ?? | всегда [] | не используется, можно вырезать | 
discounts | ?? | всегда [] | deprecated, на клиентах не парсим | *
details_screen_properties | Используется для отображения бейджика Плюса | Зависит от: а) Матчится ли cashback_for_plus, б) количества баллов на кошельке. В зависимости от этого берутся разные переводы. Подробности здесь: https://github.yandex-team.ru/taxi/backend-py3/blob/develop/services/taxi-personal-wallet/taxi_personal_wallet/api/get_available_accounts.py#L120 | deprecated, на клиентах ждем домик плюса, берём его оттуда | *
name_menu | Используется для текста Плюса в менюшке | Зависит от а) Наличия Плюса (ya_plus в pass-flags) б) баланс > 0 в) матчится эксп cashback_for_plus г) Кэшбэчный/некэшбэчный пользователь (cashback_plus в pass-flags). В зависимости от разных комбинаций этих флагов берется нужный перевод из танкера | deprecated, пока не понятно, откуда его брать на клиентах | *
subtitle | Строка с балансом “Баланс: 300 баллов” | Берем перевод из танкера, подставляем баланс | + | *
is_new | Нигде | id кошелька начинается на букву ‘z’. | Можно убрать | Нигде не используется, можно убрать | не заполняем
availability | Может предложить купить кошелёк при недоступности | None, если не payment_available, в противном случае | payment_available + тексты из танкера с константами | + | Возвращаем всегда, а не когда payment_available == False 
is_complement | Даем возмоность использовать кошелёк вместе с другими способами оплаты | сматчился экспериментмент |complement_personal_wallet_payment (сейчас всегда true для приложений с нужной версией) | + |
complement_attributes | | None, если is_complement == False, в противном случае дергает танкер для нужных строк, и вытаскивает из конфига COMPLEMENT_TYPES_COMPATIBILITY_MAPPING нужные способы оплаты для personal_wallet | + |
notification_counter | Можно вырезать, новые клиенты будут получать его из домика Плюса | если сматчился эксп cashback_for_plus в pass_flags есть ya_plus, !cashback_plus, и баланс кошелька > 0, в противном случае None | deprecated, на клиентах ждем домик Плюса |

## Скоуп задач
* [Billing] В кардсторадже отдавать кошельки
* [Taxi] В card-filter добавить модуль для обогащения кошельков
* [Taxi] Поддержать кошельки из card-filter в api-proxy и payments-eda/eats-payments
