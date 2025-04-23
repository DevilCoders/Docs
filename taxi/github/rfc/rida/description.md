# RIDA

- [rida.app](https://rida.app/)

## urls

- api.rida.app
- events.rida.app

## Handlers

### api.rida.app

В каждой(или большинстве) ручке параметры приложения передаются в query параметрах

#### pin drop
![](https://jing.yandex-team.ru/files/ulturgashev/main.jpg)

`/v1/maps/getPointInfo` - выглядит как nearestzone, но с ?уточнением? координат и определение страны.
Иногда бывают запросы с невалидными координатами. Бэк в целом, успешно такие запросы обрабатывает.

`/v1/launch` - работает в паре с `/v1/maps/getPointInfo` возвращает параметры пользователя + зоны/страны + правила отемен. Похож на `zoneinfo`

#### orders/offers
`/v1/getSuggestedPrice` - возвращает минимальную цену поездки для данных из запроса (время, расстояние, зона, страна)

`/v1/getFakeOffers` - выглядит так, что возвращает офферы в данной зоне, пока что не понял как шарится координата, так как в запросе её - нет, только зона и страна в query.
Особенности - рендерим картинки с маршрутами в jpg.

`/v1/offer/create` - создание заказа

`/v1/offer/passengerCancel` - отмена пользователем

`/v1/offer/expire` - проверка, истёк ли оффер

`/v1/offer/priceChange` - изменить цену оффера

`/v1/getOffers` - история поездок

#### auth
`/v1/auth` - авторизация, передаём номер телефона, получаем токен

`/v1/auth/verify` - подтверждение телефона, передаём код из смс и токен

`/v1/checkAuth` - проверка авторизации

`/v1/auth/updateData` - обновляет данные пользователя, язык, фотка, имя и т.д

#### settings
![](https://jing.yandex-team.ru/files/ulturgashev/settings.jpg)

`/v1/getCountryBonusData` - пункт меню - бонус, информация о бонусах (в ответе приходит html для рендеринга)

`/v1/getFaqCategories` - получение категорий для обращения в саппорт (rider/driver)

`/v1/getFaqArticle` - получить описание для категории

`/v1/getLanguages` - получить список доступных языков приложения. Вызывается при клике пункта настройки в меню

`/v1/getProfileData` - получить профиль пользователя. Вызывается при клике на профиль в меню

`/v1/setPushToken` - устанавливаем push token (токен получаем из `fcmtoken.googleapis.com`)
  
### events.rida.app

`/sub/user` - long polling
Иногда бывают проблемы с авторизацией, и в этот момент клиент начинает ддосить бэк 401 и 429 ответы

### external requests

`app.adjust.com/event` - получаем 500
