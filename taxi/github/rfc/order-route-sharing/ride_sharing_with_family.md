Кейс: хотим шарить поездки для семьи. Решили это делать в сервисе **order-route-sharing**, добавив в нём поход в **family**.


## Клиентский флоу

Клиенты вызывают `/taxiontheway` раз в 5 секунд. Расширяем запрос необязательным полем `user_actions`. В `user_actions` все ключи опциональны - отстуствие ключа, отзнает что действия не было.

```
{
    ...
    "user_actions": {
        "share_ride_with_family": {
            "value": true
        }
    }
    ...
}
```
`user_actions` с `share_ride_with_family` присылается тогда и только тогда, когда пользователь собственноручно с последнего вызова ручки переключил тоггл.


## Изменения в `/taxiontheway`

1. Добавляем поход в новую ручку `/share-with-family` (сервис **order-route-sharing**) перед походом в `/promos-on-the-way` (сервис **inapp-communications**), если хидер `X-Ya-Family-Role` имеет значение `user`.

2. После этого `/taxiontheway` ходит в `/promos-on-the-way` (сервис **inapp-communications**) с `order_id`, `sharing_key` и необязательным `share_ride_with_family`.
```
{
    ...
    "sharing_key": "e1c6a56f649ac6bea97360268d18f554",
    "order_id": "e481a19a14ffc3a8962649bd4b78fc20",
    "share_ride_with_family": {
        "value": true
    }
    ...
}
```
`sharing_key` берём из `/v1/tc/order-info` (требуется небольшая доработка сервиса **order-core** - вытащить `order.rsk` из `order_proc`).

Внутри `/promos-on-the-way` добавляем поход в новую ручку `/sharing-info` для получения состояния расшара. В соответствии с полученными данными выставляем актуальный флаг `is_selected` в баннер.


## Про кеши

В данный момент `/taxiontheway` внутри себя имеет кеш ответов ручки `/promos-on-the-way`. Нужно сделать так, чтоб при изменении значения тоггла `share_ride_with_family`-баннера кеш не использовался (другими словами при наличии в запросе `share_ride_with_family`). Про этот кеш написано здесь: https://wiki.yandex-team.ru/taxi/backend/architecture/apiproxy/manual2/#kjeshirovanieotvetovresursa. Настройки кеширования для **inapp-communications** задаются в конфиге `INAPP_TOTW_STORIES_CACHE_CONTROL`. 

### Проблема кеша

Ееш **api-proxy** (на самом деле **api-cache**) не надёжен: в любой момент алгоритм кеширования может вытеснить ответ `/promos-on-the-way`, что потенциально приведёт к сбрасыванию настроек тоггла. Клиенты не могут сделать игнорирование поля `is_selected` в тоггле при 2-3-4-... вызовах `/taxiontheway`.

### Консистентность поля `is_selected` (не актуально)

Хотели сделать асинхронные начало и конец расшара поздки, но возникло много проблем и рисков. Решили сделать синхронно, потенциально пожертвовав таймингами.

#### Вариант 0 (нельзя применять): локальный кеш в **inapp-communications**

Локальный не подходит, потому что определённое значение тоггла на клиенте должны знать все хосты. 

#### Вариант 1 (пока не будем реализовывать, воспользуемся позже при необходимости): redis

Предлагается сделать redis-кеш. Спойлер: redis **практически** не будет использоваться на чтение. Кеш **api-proxy** покрывает практически все случаи. Единственный случай, когда нужен redis-кеш - это вытеснение записи алгоритмом кеширования **api-cache**.

В redis будем складывать значения только тогда, когда пришло поле `share_ride_with_family`.

Требования:
* ttl можем установить достаточно большой, чтоб покрыть практически все поездки, например, 24h
* Количество записей - число поездок за ttl семейников. При 6h и 150 заказов/с это 1% * 3600с * 24 ~ 130k - супергрубая оценка сверху
* rps - практически нулевой (только на запись и только при наличии поля `share_ride_with_family`, то есть при изменении значения тоггла)
* При недоступности redis прекращаем расшаривание поездки и отдаём пустой список баннеров в `/promos-on-the-way`

#### Вариант 2 (отвергнут): postgresql

Уже есть бд `dbinappcommunications`, которая хранит кеш промок на карте. Изначально планировали в эту БД перевезти yql_cache, но отказались это делать год назад. Возможно, когда-нибудь и настанет время.

#### Вариант 3 (отвергнут): ничего не делать

Едва ли кеш **api-cache** будет нас часто подствалять. Можем считать, что он всегда работает корректно. Если будут обращения - реализуем один из предыдущих вариантов.


## Изменения в **order-route-sharing**

### stq __ride_sharing_with_family__ (не актуально)

Создаём новую очередь __ride_sharing_with_family__. Её stq-таски принимают в качестве аргументов `order_id`, `user_id`, `mode` (все обязательные, других аргументов не принимает). Работает в 2х режимах. 2 режима вместо 2х очередей - во избежание race conditions. Текущий механизм защищён от race conditions тем, что поездка всегда либо расшарена, либо не расшарена, и **processing** умеет трекать начало/конец поездки. 
- Режим начала расшара. Ход работы:
  1. сходить в **family** за телефонами членов семьи и информацией об админе семейного аккаунта
  2. `context.sqlt.insert_sharing_key` ---- при последующих попытках постгрес исполнит `ON CONFLICT DO NOTHING`
     `context.sqlt.insert_phone_ids`
     Т.е. шаг представляет собой работу stq __insert_order__
  3. Наполнение `order_route_sharing.family_rides`
- Режим конца расшара. Ход работы: 
  1. очистить таблицу `phone_ids`
  2. отредактировать `order_route_sharing.family_rides`

Оба режима должны быть идемпотентны.

Поскольку существующая stq __insert_order__ вызывается во всех заказах, то она оказывается в состоянии гонки с __ride_sharing_with_family__. Но тут не должно быть проблем, поскольку __ride_sharing_with_family__ выполняет в том числе и функцию __insert_order__, а __insert_order__ идемпотентна. Порядок выполнения __ride_sharing_with_family__ и __insert_order__ не важен - результат будет как у одной лишь __ride_sharing_with_family__.

### БД

Добавляем таблицу `order_route_sharing.family_rides`:
```
CREATE TABLE order_route_sharing.family_rides (
    sharing_key NOT NULL REFERENCES order_route_sharing.sharing_keys(sharing_key) ON DELETE CASCADE,
    admin_uid UNIQUE INTEGER NOT NULL, -- из ответа сервиса family
    admin_name VARCHAR NOT NULL, -- из ответа сервиса family
    sharing_on BOOLEAN NOT NULL -- выставляется в соответствии с последним модом "ride_sharing_with_family"
)
```

### Ручка `GET /sharing-info` - новая ручка

Request:
```
{
    "sharing_key": "e1c6a56f649ac6bea97360268d18f554"
}
```

Response:
```
{
    "phone_ids": ["5db2bb01211473c8c34f358d"], // список телефонов, на которые расшарена поездка
    "family": { // Отсутствует, если человек не состоит в семье
        "admin_name": "Василий",
        "admin_uid": 393627008,
        "sharing_on": true
    }
}
```

По данному `sharing_key` ищем информацию в таблицах `order_route_sharing.phone_ids`, `order_route_sharing.family_rides` (см. об изменениям в базе далее).

### `POST /share-with-family` - новая ручка

Ручка добавляет или обновляет информацию о поездке, которую шарят членам семьи. 

Request:
```
{
    "order_id": "e481a19a14ffc3a8962649bd4b78fc20",
    "sharing_key": "e1c6a56f649ac6bea97360268d18f554",
    "share_ride_with_family": {
        "value": true
    }
}
```

Response:
```
{}
```

Общая работа ручки (2 режима: начало расшара и конец расшара):
- Режим начала расшара. Ход работы:
  1. сходить в **family** за телефонами членов семьи и информацией об админе семейного аккаунта
  2. `context.sqlt.insert_sharing_key` ---- при последующих попытках постгрес исполнит `ON CONFLICT DO NOTHING`
     `context.sqlt.insert_phone_ids`
     Т.е. шаг представляет собой работу stq __insert_order__
  3. Наполнение `order_route_sharing.family_rides`
- Режим конца расшара. Ход работы: 
  1. очистить таблицу `phone_ids`
  2. отредактировать `order_route_sharing.family_rides`

### Ручка `GET /v1/info` - уже существует, доработка

Поле `popup_title` при условии `admin_name NOT NULL` заполняем новой подписью с участием поля `admin_name`.


## Изменения в **family**

Добавляем новую ручку получения информации о семье: её админе и членах.

