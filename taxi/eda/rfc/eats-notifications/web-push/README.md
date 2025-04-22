# Веб пуши

## Проблема:

#### Нужно уметь отправлять пользователю уведомления в браузер:

1. Нужно уметь подписывать пользователя на веб-пуши
2. Нужно уметь отписывать пользователя от веб-пушей
3. Нужно уметь хранить данные о подписке пользователя
4. Нужно уметь отправлять пользователю веб-пуши

## Решение:

### Подписка пользователя на веб-пуши

Для подписки пользователя на веб-пуши нужно будет завести еще одну ручку.
Заведем ручку `/v1/subscribe/webpush`

Спеку описываем согласно документации ксивы: https://console.push.yandex-team.ru/#api-reference-subscribe-webpush
Вот тут описано, как и что клиент получает от браузера: https://rossta.net/blog/using-the-web-push-api-with-vapid.html#triggering-a-web-push-notification

От клиента нам нужно уметь получать json с данными, необходимыми для подписки:
```json
{
  "subscription":  {
    "endpoint": "https://android.googleapis.com/gcm/send/a-subscription-id",
    "keys": {
      "auth": "AEl35...7fG",
      "p256dh": "Fg5t8...2rC"
    }
}
```

Для получения `user_id` нам нужен авторизационный контекст. 

```yaml
    /v1/subscribe/webpush:
        post:
            description: Подписка браузера на веб-пуши
            x-taxi-middlewares:
                eats: v1
            requestBody:
                required: true
                content:
                    application/json:
                        schema:
                            type: object
                            additionalProperties: false
                            properties:
                                subscription:
                                    $ref: '../definitions.yaml#/components/schemas/WebPushSubscription'
                            required:
                              - subscription
            responses:
                204:
                    description: Браузер успешно подписан на веб-пуши

    WebPushSubscription:
        description: содержит данные о подписке пользователя
        type: object
        additionalProperties: true
```

Сохранение девайса реализуется через STQ аналогично текущему флоу работы с физическим девайсом. Реализовать подписку лучше в другой очереди, потому что сильно различаются параметры, которые мы хотим в нее передать.

Для того, чтобы управлять подпиской нам нужно хранить параметр `session`, который служит идентификатором клиента при подписке/отписке, позволяет обновить данные существующей подписки и отправить уведомление в конкретную сессию подписки. В качестве `session` подойдёт любая строка, уникально идентифицирующая браузер. Для этих нужд будем использовать `device_id`, так как он сейчас используется во всех клиентах `eats-notifications` для отправки нотификации на определенное устройство.

### Отписка пользователя от веб-пушей

Для отписки нужно сделать еще одну ручку: `/v1/unsubscribe POST`. 

```yaml
    /v1/unsubscribe:
        post:
            description: Отписка от пушей
            x-taxi-middlewares:
                eats: v1
            requestBody:
                required: true
                content:
                    application/json:
                        schema:
                            type: object
                            additionalProperties: false
                            properties:
                                application:
                                    type: string
                            required:
                              - application
            responses:
                204:
                    description: Задача на отписку пользователя принята
```

Для отписки нам нужно иметь `device_id`, который мы имеем вместо `session`, и `user_id`. Их мы достаем из авторизационного контекста. В теле запроса для отписки от веб-пушей нужно передавать `eda_web`.

Отписку можно реализовать через новую очередь `eats_notifications_unsubscribe`. 

```yaml
name: eats_notifications_unsubscribe
arguments:
  - name: eater_uuid
    schema:
        type: string
  - name: eater_id
    schema:
        type: string
  - name: device_id
    schema:
        type: string
  - name: application_key
    schema:
        type: string
```


### Хранение данных о подписке пользователя

Данные о подписке пользователя можно хранить в той же табличке и в том же формате. Табличку `user_devices` можно будет расширить полем `device_type`, которое будет показывать, какой это девайс.


### Отправка пользователю веб-пушей

Отправка сообщения сильно не меняется. Если включена отправка пуша и смс, то, если отправили веб-пуш, **дублируем его в смс**.

Нужно будет описать соответствующее приложение в конфиге `EATS_NOTIFICATIONS_APPLICATIONS_V2`. В нем же будем определять логику дублирования.
