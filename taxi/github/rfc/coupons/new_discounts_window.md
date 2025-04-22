# Общее описание

## Что
Обновленный экран скидок, изменения в рефералке

## Дизайны
https://www.figma.com/file/vulslXtA8NvRA5hLWxeQhP/Реферальная%E2%80%A8-программа

## Тикеты
https://st.yandex-team.ru/TAXIWORLD-204

https://st.yandex-team.ru/TAXIBACKEND-41095

## Описание
* Экран скидок разбивается на 2 раздела: Active Discounts, Inactive Discounts.
  * Active Discounts - те скидки, что и сейчас отображаются в этом разделе,
т.е. те, что активированы текущим юзером
  * Inactive Discounts - "будущие" скидки, т.е. те скидки, которые получит юзер в
награду за рефералку. Отображается по одной скидке-награде за каждый
активированный промокод-инвайт ребенком
* Оба раздела так же, как и сейчас разбиваются в свою очередь по сервисам
(taxi, grocery)
* У скидок отображается картинка с машинкой: если скидка на конкретный тарифный
класс, то будет машинка из тарифа, по дефолту - обычная желтая машинка

![image](static/new_discounts_window.png)

# Изменения на бекенде

## (A) Возможность давать награду родителю после N-й поездки
сейчас награду даем безусловно после первой поездки

Что нужно поменять:
* Миграция таблички `creator_configs` - добавляем новое поле `rides_for_reward`
(дефолт 1; число поездок ребенка по промокоду, для получения награды родителем)
* Миграция таблички `referral_completions` - добавляем новое поле
`completed_rides` (совершенные поездки по этому промокоду)
* Меняем код `complete_referral` (ручка и stq-таска), инкрементим
`completed_rides`, сравниваем `completed_rides`  с `rides_for_reward`,
чтобы проверить условия необходимости наградить родителя
* Меняем код админки (check-ручки), добавляем проверку, что серия реферального
промокода (give-часть, для ребенка) выдает награду на N поездок,
где `N >= rides_for_reward` (т.к. у нас важно совершить N поездок
именно по промокоду от родителя)
* Исходя из предыдущего пункта нужно добавить новое поле в админку
рефералки (фронт)

## (B) Выводить в списке скидок родителя будущие реферальные промокоды-награды
так называемые "неактивные" скидки. Они будут в своем отдельном разделе
(Inactive discounts), ниже раздела обычных (Active) скидок

Добавляем вывод в ручку `coupons_list`.
Возвращаем в корне ответа массив `inactive_coupons`, по аналогии с `coupons`
из ответа, но без многих полей (например, нет `code` , т.к. мы ещё не выдали
промокод, это будущая награда, см. ниже yaml)
Отдавать `inactive_coupons`  лучше по какому-то флажку в запросе, чтобы
там где не надо не увеличивать время ответа

`image_tag` нужно также возвращать и в поле `coupons`  ручки `coupons_list`,
т.к. теперь у всех скидок будет картинка

### diff в спеке

формат запроса в `coupons_list`:
```yaml
--- taxi/uservices/services/coupons/docs/yaml/api/coupons_list.yaml     (index)
+++ taxi/uservices/services/coupons/docs/yaml/api/coupons_list.yaml     (working tree)
@@ -65,6 +65,12 @@ definitions:
                     description: Сервисы, хотя бы к одному из которых должен принадлежать
                         промокод, чтобы попасть в ответ. По умолчанию -  ['taxi']
                     example: ['taxi', 'grocery', 'eats']
+                inactive_coupons:
+                    type: boolean
+                    description: |
+                        включать ли в ответ неактивные купоны
+                        (будущие награды за рефералку, когда выполнятся
+                        условия рефералки)
                 version:
                     type: string
                     description: строка версии user_coupons на клиенте
```

формат ответа в `coupons_list`
```yaml

--- taxi/uservices/services/coupons/docs/yaml/api/coupons_list.yaml     (index)
+++ taxi/uservices/services/coupons/docs/yaml/api/coupons_list.yaml     (working tree)
@@ -76,6 +76,10 @@ definitions:
                 type: array
                 items:
                     $ref: '../definitions.yaml#/definitions/Coupon'
+            inactive_coupons:
+                type: array
+                items:
+                    $ref: '../definitions.yaml#/definitions/InactiveCoupon'
             ui:
                 type: object
                 additionalProperties: false
--- taxi/uservices/services/coupons/docs/yaml/definitions.yaml  (index)
+++ taxi/uservices/services/coupons/docs/yaml/definitions.yaml  (working tree)
@@ -474,6 +474,9 @@ definitions:
                 type: string
                 description: дополнительная информация о промокоде
                 example: За поездку друга по вашему реферальному коду
+            image_tag:
+                type: string
+                description: тег картинки, отображаемой рядом со скидкой
             currency_rules:
                 $ref: '#/definitions/CurrencyRules'
             action:
@@ -487,6 +490,37 @@ definitions:
           - title
           - currency_rules

+    InactiveCoupon:
+        type: object
+        additionalProperties: false
+        properties:
+            service:
+                description: сервис, к которому принадлежит промокод
+                type: string
+                example: "taxi"
+            reason:
+                description: причина неактивности промокода
+                type: string
+                example: "A friend has to make 2 more trips"
+            title:
+                type: string
+                example: "10% for 4 trips"
+            subtitle:
+                type: string
+                description: дополнительная информация о промокоде
+                example: "All tariffs Until December 31, 2022"
+            image_tag:
+                type: string
+                description: тег картинки, отображаемой рядом со скидкой
+            currency_rules:
+                $ref: '#/definitions/CurrencyRules'
+            action:
+                $ref: '#/definitions/CouponAction'
+        required:
+          - reason
+          - title
+          - currency_rules
+
     UserError:
         type: object
         additionalProperties: false

```

Для того, чтобы получить `inactive_coupons`, нам надо поселектить
`referral.promocodes` по данному юзеру, подтянуть `promocode_activations`,
`promocode_success_activations`,
`referral_completions`, `creator_configs`. И выбрать промокоды:
1) для которых есть успешная активация, но нет completion,
2) для которых есть completion, но поездок совершено меньше чем
`rides_for_reward`. Число таких заселекченных активаций - число
неактивных промокодов. Для каждого по `creator_configs` мы подтянем
описание скидки и отдадим в ответ. Также отдаем в ответ оставшееся
число поездок для награды

число активаций без завершения поездки:
```sql
WITH user_referral_promocodes AS (
SELECT
  rp.id,
  rp.yandex_uid
FROM referral.promocodes rp
), activations_wo_completions AS (
SELECT
  urp.id AS promocode_id,
  count(*)-count(rrc.id) AS count
FROM referral.promocode_success_activations rpsa
JOIN referral.promocode_activations rpa
  ON rpa.id = rpsa.activation_id
JOIN user_referral_promocodes urp
  ON urp.id = rpa.promocode_id
LEFT JOIN referral.referral_completions rrc
  ON (rrc.promocode_id = urp.id
  AND rrc.yandex_uid = rpsa.yandex_uid)
GROUP BY
  urp.id
)
SELECT * FROM activations_wo_completions;
```

## (C) Возможность делиться промокодом-наградой
Любым промокодом можно делиться, если сделать `coupon/deactivate`,
а затем `coupon/activate`, но т.к. это 2 операции разнесенные по времени
(нажаться "share" у одного клиента и применить промокод у другого клиента),
то возникают проблемы с транзакционностью.

Видимо нужно помечать промокод, которым поделился клиент1
(готовность отдать промокод).
Тогда когда происходит активация промокода у клиента2,
то можем посмотреть в эту пометку и перепривязать промокод одной
транзакционной операцией. Следовательно нужна ручка для клиента,
дергаемая по клику на share. Навскидку помечать промокоды можно
прямо в коллекции `promocodes`

Нужна бизнес-проработка, какими скидками можно делиться.
Насколько далеко можно делиться, т.е. можно ли скидки передаривать дальше
и дальше.

Делаем после пп. (A), (B)

## (D) Возможность послать пуш детям, которые активировали промокод, но не совершили поездку
Новая ручка, которая выселекчивает таких юзеров
(postgresql-таблички в бд `referral`) и отправляет им пуш.
Ручку дергает клиент при нажатии "remind all".
Нужно отслеживать частотность отправки, не позволять отправлять пуши часто,
не позволять ручке заспамить клиентов (наскидку заводим табличку для
отслеживания этого).
Пуш с бека - через хождение в `client-notify`.

Делаем после пп. (A), (B)
