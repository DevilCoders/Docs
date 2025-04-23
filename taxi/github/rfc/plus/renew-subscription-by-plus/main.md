# Проработка "Хочу продлевать подписку через плюс"
## Продуктовое описание
Хотим дать пользователю возможность продлевать подписку через баллы Плюса, для этого добавить переключатель "Продлевать подписку баллами". 

![Продлевать подписку через плюс](./images/renew.jpg)

Продление подписки за баллы происходит только в том случае, если пользователь уже продлевает подписку за счет какого-то другого способа оплаты. Если не получится продлить подписку за баллы, продлевать нужно будет за счет основного способа оплаты. Если пользователь отказался в принципе продлевать подписку, согласие продлевать за баллы не должно форсировать покупку.

## Анализ
Сейчас продление подписки для плюса и музыки реализованы на стороне Траста, списание средств с кошелька так же работает через траст, поэтому, скорее всего, продление подписки за баллы так же будет реализовываться на стороне траста. С нашей стороны на первом этапе нужно дать понять, что пользователь согласился продлевать подписку баллами.

## Решение
Предлагаю следующие изменения:
### Для сервисов Яндекса
Добавить две ручки в сервис `plus`, которые сохраняют/отдают данные о настройках пользователя.

```
GET /v1/subscriptions/settings?yandex_uid=<uid>
```
Response:
```json
{
    "settings": {
        "renew_subscription_by_plus": false,
    },
    "version": "1"
}
```

```
PUT /v1/subscriptions/settings?yandex_uid=<uid>
```
Request:
```json
{
    "settings": {
        "renew_subscription_by_plus": true,
    },
    "version": "1"
}
```
Response:
```json
{
    "settings": {
        "renew_subscription_by_plus": true,
    },
    "version": "2"
}
```
`version` передаётся для избежания проблем с гонками. Флоу такой: Получили `version` из ручки, изменили нужные настойки, пошли в ручку с тем же `version`

Ручки будут ходить в базу, и хранить настройки в ней. Предлагаю следующую схему для базы:

```sql
CREATE TABLE plus.user_settings
(
  yandex_uid                   TEXT  NOT NULL,
  version                      TEXT  NOT NULL,
  renew_subscription_by_plus   BOOL  NOT NULL,
  PRIMARY KEY (yandex_uid)
);
```
При добавлении новых настроек будем проводить миграции, и добавлять новые поля

### Для клиентов
Добавить в ручку [/internal/v1/subscriptions/list](https://github.yandex-team.ru/taxi/uservices/blob/develop/services/plus/docs/yaml/api/launch.yaml#L16) новое поле:

```diff
      manage_url:
        type: string
        description: URL для управления подписками
      active_subscriptions:
        description: Активные пользовательские подписки
        type: array
        items:
          $ref: '#/definitions/ActiveSubscription'
      allowed_subscriptions:
        description: Доступные для оформления подписки
        type: array
        items:
          $ref: '#/definitions/AllowedSubscription'
      promoted_subscriptions:
        type: array
        description: Подписки которые нужно продвигать клиенту
        items:
          $ref: '#/definitions/PromotedSubscription'
      pending_purchases:
        type: array
        description: Идентификаторы заказов находящихся в статусе pending
        items:
          type: string
          example: 453fadadadff4f4ff5f4feeee
+     subscriptions_settings:
+       $ref: '#/definitions/SubscriptionsSettings'

definitions:
+  SubscriptionsSettings:
+    type: object
+    description: Пользовательские настройки в отношении подписок
+    required:
+      - version
+      - settings
+    properties:
+      version:
+        type: string
+        example: "3"
+      settings:
+        $ref: '#/definitions/Settings'
+
+  Settings:
+    type: object
+    properties:
+      renew_subscription_by_plus:
+        $ref: '#/definitions/RenewSubscriptionByPlus'
+      
+  RenewSubscriptionByPlus:
+    type: object
+    description: Хочу продлевать подписку за плюс
+    required:
+      - title
+      - current_value
+    properties:
+      title:
+        type: string
+        example: Продлевать подписку баллами
+      currnet_value:
+        type: boolean
+        description: Текущее значение флажка.
```
которое через `launch` попадет клиентам. Так же добавить клиентскую ручку для изменения настроек:

```
PUT /4.0/plus/v1/subscriptions/settings
```
Request:
```json
{
    "settings": {
        "renew_subscription_by_plus": true,
    },
    "version": "2"
}
```
Response:
```json
{    
    "settings": {
        "renew_subscription_by_plus": true,
    },
    "version": "3"
}
```
Клиентская ручка не будет возвращать 409 при конфликтах, а будет их резолвить, так как в случае бинарного флажка разрулить конфликт не является проблемой. Делаем так в целях оптимизации, чтобы при показе домика Плюса не ходить в ручку получения актуального стейта, а также переложить простую работу по устранению конфликтов на бэк. Если будут добавляться не булевы поля, могут начаться проблемы с синхронизацией, тогда уже возможно придётся отвечать 409 и добавлять клиентскую ручку для чтения актуального стейта.

## Предполагаемая нагрузка
Кто будет ходить в ручку для чтения флажка:
* Траст, чтобы узнать, нужно ли продлевать подписку через плюс. На данный момент равномерно в течение года происходит ~2млн продлений подписок, это ~0,06 rps.
* Паспорт. Ему нужно уметь читать и изменять эти настройки. Сейчас примерно 20к посещений паспорта в день, ~0.5 rps
* Лэндинг плюса, ориентировочно так же не сильно много, на уровне паспорта
* Возможно, админка, если её будут делать. Нагрузка вообще незначительная

Кто будет ходить в ручку записи флажка:
* Паспорт. В разы реже, чем читать, поэтому там десятые или сотые доли rps.
* Возможно, админка.

Клиентская ручка:
* Домик плюса, оцениваем не очень много, в районе ~1 рпс.

Количество записей в таблице:

Сейчас подписчиков плюса ~4 млн, через год планируется поднять планку до ~8 млн, продлевают подписку примерно половина, поэтому, оцениваю количество записей на старте примерно ~ 4 млн, со временем это количество, скорее всего, будет сильно расти.

## Разработка
### Необходимый список задач, для корректной работы:
1) Добавить внутренниюю ручку GET `settings` в сервис `plus`, Здесь же завести базу. (2d)
2) Добавить ручку PUT`settings` в сервис `plus` (2d)
3) Ручка `/internal/v1/subscriptions/list` - добавить новое поле с настройками (1d)
4) Пользовательская ручка `/4.0/plus/v1/subscriptions/settings/` (2d)
