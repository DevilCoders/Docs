# Проксирование пуш-уведомлений винда

## Задача
Существуют [сценарии](https://docs.google.com/spreadsheets/d/1GLQytYoOaNHgifATMKDizHfud7SXCCW5JBSfOXumMS8/edit#gid=1941068542), когда Wind хочет послать пользователю push-уведомление.
При этом, если поездка совершена/совершается через Yango, пуш должен прилететь в Yango.
Хочется предусмотреть возможность "замалчивания" или "переопределения" каких-то пушей.

## Как делаем
Даем винду ручку, которую они будут дергать, когда надо отправить пользователю пуш. В эту ручку они будут передавать все данные о пуше, а мы уже будем переупаковывать это в свои пуши и посылать через ucommunications.

### Изменения в таблице users
Для отправки пуш-уведомлений через ucommunications нужно знать таксишный user_id.
Предлагаю сохранять его в таблицу users в ручке /sesions/current, которая начинает поллиться
с момента открытия приложения при условии включенного экспа scooters.

Плюс будем обновлять этот user_id в базе всякий раз когда он будет меняться (т.е. пуши будем слать на последний использованный девайс)

Нам также надо сохранять локаль пользователя для переводов текстов уведомлений
при отправке пушей.

Новые поля в таблице users:
```json5
{
    "yandex_user_id": "...",
    "locale": "ru/en/..."
}
```

### Ручка POST /talaria/v1/notifications/push
В запросе к ручке ожидаем следующие хедеры:
- X-Idempotency-Token - ключ идемпотентности для отправки пуша
(**TODO** уточнить с виндом и не забыть в коде залогировать, тк хедеры не логируются)

И request body:
```json5
{
    "wind_user_id": "...",
    "notification": {
        "id": "autoLockFinishRideFailed", // notification type

        // all other fields are optional for now, maybe need them, maybe not
        // as we are very likely to use our own texts, actions etc.
        "is_shown_in_active": false, // show in-app popup when the app is in the foreground.
        "action": "...", // some action on notification tap, we can convert to action/deeplink
    }
}
```

В ручке достаем из базы yandex_user_id по wind_user_id, получаем из конфигов/экспов
необходимые данные для каждого типа пуша и отправляем пуш через ucommunications.
**TODO:** тут детали еще будут после обсуждения с менеджером и клиентами

Ответ ручки http response 200 ok.
Возможно, имеет смысл завернуть вызов ucommunications в stq таску,
чтобы можно ретраить в случае ошибок, но кажется что это скорее будет оверкилл.
( + у нас нет гарантий доставки в любом случае, так что не нужно)

### Конфиг 3.0 для пушей
Заведем конфиг 3.0 для настроек и данных по различным видам пушей в виде мапы:
notification_id -> настройки и данные для пуша

Примерно так:
```json5
{
    "autoLockFinishRideFailed": {
      "enabled": true, // so that we can mute notifications without deleting them from config
      "title": "tanker_key",
      "subtitle": "tanker_key",
      "deeplink": "taxi://...",
      // ... some other fields
    },
    // ... other notification types
}
```

## Вопросы к винду
1. Могут ли они сами определять поездки, которые проходят через янго (например, по источнику запросов в их ручки), и только для поездок через янго дергать нашу ручку для проксирования пушей?
