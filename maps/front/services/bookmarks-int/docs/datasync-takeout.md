# Datasync Takeout API

API для удаления пользовательских данных из баз данных DataSync, которые относятся к Яндекс.Картам.

ПД - пользовательские данные

## Общие положения

### Сервисы-потребители

Потребители сервиса:

- Takeout ([ABC](https://abc.yandex-team.ru/services/takeout/))

### Авторизация

Все клиенты авторизуются с помощью [юзер-тикетов](https://wiki.yandex-team.ru/passport/tvm2/user-ticket/) и [сервис-тикетов](https://wiki.yandex-team.ru/passport/tvm2/stbrief/) TVM 2.0.

### Список ПД в DataSync

* bookmarks - закладки
* search-history - поисковая история
* points-history - конечные точки маршрутов
* addresses - адреса дом, работа и др
* ridehistory - история поездок
* ynavisync - данные для связи приложения Нави и ГУ, использует в Я.Драйв и Я.Авто
* ynavicarinfo - номера машин, Vin - для отзывных компаний

## Упрощенная схема работы

### Запрос статуса ПД в DataSync:

1. пользователь открывает страницу статусов своих ПД в Паспорте
2. Паспорт (сервис Takeout) делает запросы в различные сервисы за статусами ПД (один из запросов в bookmarks-int)
3. bookmarks-int делает несколько запросов (соотвественно списку ПД) в Cloud Api за информацией о БД
4. после получения и обработки данных bookmarks-int возвращает ответ для сервиса Takeout
5. пользователь видит статусы

### Удаление ПД в DataSync:

1. пользователь открывает страницу статусов своих ПД в Паспорте и выбирает какие данные хочет удалить (в данном случае из списка ПД выше)
2. Паспорт (сервис Takeout) делает запрос в bookmarks-int на удаление ПД по ключу из списка ПД
3. bookmarks-int делает несколько запросов (соотвественно списку ПД) в Cloud Api на удаление БД
4. после завершения запросов bookmarks-int возвращает ответ для сервиса Takeout

## Варианты использования

Ручки соответствуют описанным [требованиям](https://wiki.yandex-team.ru/users/yakushevsky/takeoutrequirements/).

## Полезные ссылки

1. [Personality ручки](https://wiki.yandex-team.ru/disk/personality/)
2. [DataSync API](https://yandex.ru/dev/datasync/http/doc/dg/concepts/authorization.html)
3. [Как происходит удаление БД в DataSync](https://st.yandex-team.ru/MAPSHTTPAPI-2476#61e1350ab328d50f585b5072)
