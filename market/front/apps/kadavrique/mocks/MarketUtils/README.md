# MarketUtils - сравнения и подписки на рассылки

[Документация](http://market-utils.tst.vs.market.yandex.net:35826/api/swagger-ui.html#/)

## Сравнения

## GET /api/comparison/categories/count - получить кол-во категорий сравнений
## GET /api/comparison/<userIdType>/<userId> - получить категории сравнений
## DELETE /api/comparison/<userIdType>/<userId>/product/<productId> - удалить товар из сравнения

## Подписки

## GET `/api/subscription/` - получить подписки
## POST `/api/subscription/` - создать подписку
## DELETE `/api/subscription/<id>` - удалить подписку

Поддерживаемые статусы подписок
+ CONFIRMED
+ NEED_SEND_CONFIRMATION

Поддерживает параметры:
+ yandexUid – идентификатор пользователя

## Получить настройки пользователя (в формате попапа)
## GET `/api/settings/email/notifications/context`

Параметры в query:

`uid` - UID пользователя

## Сохранить настройки пользователя
## POST `/api/settings/email/notifications/context`

Параметры в query:

`uid` - UID пользователя
`email` - e-mail пользователя

Параметры в теле:

`ad`: ?boolean, подписка на рекламу
`wishlist`: ?boolean, подписка на вишлист
`grade`: ?boolean
`forum`: ?boolean

`place`: ?string идентификатор блока (footer, settings-popup, etc)
`platform`: ?string идентификатор платформы (desktop, touch, corner)

## POST /api/verification/ - подтвердить подписку / отписку

## POST /api/unsubscribe-reason/ - создать причину отписки
