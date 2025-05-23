# Новый принцип полинга данных активных заказов в приложении Такси

## Цель

Оптимизировать полинг данных, в частности в ручке taxiontheway, с прицелом на суперапп.
Отделить данные, критичные для цикла заказа от некритичных.
Определить способ получения данных от микросервисов фич таким образом, чтобы не требовалось перезапрашивать неизменённые данные при каждом запросе поллинга.

## Принципы

- критичные данные должны отдаваться всегда, второстепенные данные (и сервисы) не должны мешать основному флоу заказов
- критичные ручки не должны отдавать много лишних данных - чтобы при медленной сети они не стали блокером для цикла заказа

## Общая концепция (подробности ниже)

1. На запуске приложения короткая информация обо всех активных заказах возвращается в ответе ручки launch в поле `sa_orders_state`.
1. Далее, если есть известные незавершённые заказы, поллится новая ручка `/mlutp/v1/orders/state`. В этой ручке приходит короткий статус по заказу, а так же информация, нужно ли сходить за новыми подробными данными по заказу.
1. Клиент идёт за подробными данными по заказу по правилу поллинга.

### Варианты реализации

1. Одна ручка поллинга с переменным количеством данных. Backend определяет, какие данные просрочены на клиентах, сам собирает их из источников и отдаёт клиентам.
    Преимущества:

    - реализация разбиения и кеширования максимально скрыта от клиентов;
    - на клиентах достаточно реализовать только частичное обновление локального представления;
    - возможность гибко и незаметно от клиентов менять разбиение на парты.

    Недостатки:

    - очень нестабильные тайминги ручки;
    - при проблемах с некритичным сервисом замедляется весь полинг;
    - риск при неправильной конфигурации некритичного сервиса сломать критичные части и весь полинг;
    - необходимость реализовывать более сложную обработку необязательных полей (чтобы отличить кейс когда клиентский кеш валиден от кейса когда опциональное поле нужно удалить).

1. *В этом и следующих вариантах ручка полинга отдаёт необходимость дозапросить информацию в других ручках.*
Фиксированное разбиение totw на части.
    Преимущества:

    - простая реализация на клиентах;
    - очень быстрая ручка полинга *(здесь и в следующих вариантах)*;
    - возможность отделить некритичные и критичные данные по разным ручкам *(здесь и в следующих вариантах)*.

    Недостатки:

    - необходимость на первом этапе разбить данные о заказе на ручки;
    - невозможность поменять разбиение в будущем без перевыкатки клиентов;
    - практически нет возможности реализовать итеративно.

1. *Здесь и далее рассматривается динамичское разбиение на парты.*
Клиенты ничего не знают о разбиении, обновляют все поля пришедшие в ответе ручки полинга. Все текущие опциональные поля нужно распределить в неопциональные объекты. Отсутствие объекта означает что данные в клиентском кеше актуальны, наличие означает что нужно обновить данные по всем полям, которые в нём ожидаются.
    Преимущества:

    - возможность гибко менять разбиение данных о заказе на части *(здесь и в следующих вариантах)*;

    Недостатки:

    - нужно 44 опциональных поля сразу сгруппировать на неделимые части;
    - нужно на клиентах на первом этапе реализовать более сложную логику склеивания данных из частей *(здесь и в следующих вариантах)*.

1. Клиенты знают, какие поля должны приходить в какой ручке дополнительной информации, но это распределение приходит с бекенда на старте.
    Преимущества:

    - можно гарантировать, что поля на верхнем уровне не пресекаются (это гарантируется при отдаче правил полинга)
    - не меняется логика работы с опциональными полями

    Недостатки:

    - на клиентах нужно реализовать обновление только тех полей, которые ожидались в ручке.

Далее рассматривается последний вариант.

### Polling policy

Это набор правил о том как получить данные о заказе. Приходит в ответе launch.

Каждое правило содержит:

- имя сервиса для которого оно применимо,
- имя части данных о заказе (парта), чтобы понимать какой тег относится к парту,
- url ручки в которой запрашивать данные,
- список полей которые должна отдавать ручка (при изменении списка нужно поднимать версию ручки на бекенде),
- тип поллинга: `route_distance_depended` для поллинга по правилам `taxiroute` и `tag_defined` для поллинга по тегу,
- идентификатор формата запроса и ответа: `part_type`: ка клиентах нужно иметь соответствие этого типа и формата запроса и формат ответа из ручек полинга, а так же какую часть внутреннего представления данных о заказе нужно менять по ответу из этой ручки. Незнакомые `part_type` нужно игнорировать,
- приоритет запроса парта `priority`: если не удаётся сделать запросы параллельно, то нужно делать сначала запросы с меньшим значением этого поля,
- флаг необходимости дождаться ответ парта `required`: если в ответе поллинга пришла информация что такой парт нужно запросить, не меняем ui пока не дождёмся ответа по нему. Нужен для согласованного изменения данных о заказе, например когда изменение статуса предполагает изменение ui, данные для которого придут в одном из партов.

Как поменять правила поллинга:

1. заводим новые ручки с новым распределением полей между ними,
1. начинаем отдавать polling_policy с новыми ручками и новым списком полей для каждой из них. Если при этом в кеше тегов по партам (на бекенде) уже есть информация о заказе, нужно инвалидировать её,
1. клиенты, у которых уже есть polling_policy, пользуются старыми ручками,
1. как только rps на старые ручки упадёт до 0, их можно выключить,
1. на клиентах при получении нового polling_policy нужно обязательно использовать его.

## Ручки

### Изменения в launch

В запрос этой ручки добавляем поля:

```json
{
    "supported_services": ["taxi","eats","grocery","etc..."],
    "known_orders": [
        {
            "orderid": "order1",
            "tags": {
                "fast_info": "encoded_tags",
                "part2": "encoded_tags"
            },
            "service": "taxi",
            "status": "driving"
        },
        {
            "orderid":"order1",
            "tags": {
                "full_info": "encoded_tag"
            },
            "service": "eats",
            "status": "cooking",
            "some_field": "some_value"
        }
    ]
}
```

Первый параметр нужен для того, чтобы понимать, из каких сервисов доставать список известных заказов.

Второй параметр опциональный, он позволит сразу проверить валидность локального кеша а так же будет использоваться для [фолбека в случае недоступности сервиса](#Недоступность-источника-заказов).

В ответе в поле `mlutp_orders_state` придут следующие данные

```json
"mlutp_orders_state": {
    "orders":[
        {
            "orderid": "order_1",
            "service": "taxi",
            "status": "driving",
            "tags": {
                "fast_info": "encoded_tag",
                "part2": "encoded_tag"
            },
            "need_request": ["fast_info", "part2"],
            "update_status": "actual"
        },
        {
            "orderid": "order_1",
            "service": "eats",
            "status": "cooking",
            "some_field": "some_value",
            "tags": {
                "full_info": "encoded_tag"
            },
            "need_request": [],
            "update_status": "stale"
        }
    ],
    "allowed_changes": [
        {
            "service": "taxi",
            "can_make_more_orders": true
        },
        {
            "service": "eats",
            "can_make_more_orders": false,
            "no_more_orders_reason": "reason"
        }
    ],
    "polling_policy": [
        {
            "service": "taxi",
            "part_name": "fast_info",
            "url": "/4.0/taxi/order/fast",
            "fields": ["field1", "field2", "field3"],
            "polling_type": "tag_defined",
            "part_type": "totw",
            "priority": 2,
            "required": true
        },
        {
            "service": "taxi",
            "part_name": "part2",
            "url": "/4.0/part2",
            "fields": ["field1", "field2", "field3"],
            "polling_type": "tag_defined",
            "part_type": "totw",
            "priority": 3
        },
        {
            "service": "taxi",
            "part_name": "route",
            "url": "/4.0/taxiroute",
            "fields": ["taxiroute"],
            "polling_type": "route_distance_depended",
            "part_type": "taxiroute",
            "priority": 1
        },
        {
            "service": "eats",
            "part_name": "full_info",
            "url": "/some/eats/url",
            "fields": ["field1", "field2", "field3"],
            "polling_type": "tag_defined",
            "part_type": "eats_full",
            "priority": 4,
            "required": true
        }
    ]
}
```

Если заказ не пришёл, значит он не активен и по нему не ожидается оценка.
Для заказов с `"update_status": "stale"` нужно показать лоадер и дёргать ручку полинга, пока не придут данные. В ответ для таких заказов придут те же данные о заказе, которые пришли в запросе от клиента (в примере выше это `status` и `some_field`).
Это нужно чтобы в случае проблем с сервисом у пользователя не пропали только что созданные заказы, и он не начал создавать дубли.
Так как данные для `need_request` в будущем будем брать из отдельного сервиса, может быть ситуация когда в `need_request` пришли парты, но при этом статус информации `stale`. В таком случае нужно игнорировать `need_request`.

### Полинг заказов

Нужна для поллинга изменения состояния заказа.

`/mlutp/v1/orders/state`

Отдаёт короткую информацию о запрошенных заказах и имена партов, которые нужно обновить.

request:

```json
{
    "known_orders": [
        {
            "orderid":"order1",
            "tags": {
                "fast_info": "encoded_tag",
                "part2": "encoded_tag"
            },
            "force": true,
            "service": "taxi",
            "status": "searching"
        },
        {
            "orderid":"order1",
            "tags": {
                "full_info": "encoded_tag"
            },
            "force": false,
            "service": "eats",
            "status": "cooking",
            "some_field": "some_value"
        }
    ]
}
```

`known_orders` – упорядоченный массив. Порядок такой как сейчас отображается в интерфейсе.

response:

```json
{
    "orders": [
        {
            "orderid": "order_1",
            "service": "taxi",
            "status": "driving",
            "need_request": ["fast_info"],
            "tags": {
                "fast_info": "encoded_tag",
                "part2": "encoded_tag"
            },
            "update_status": "actual"
        }

        {
            "orderid": "order_1",
            "service": "eats",
            "status": "cooking",
            "some_field": "some_value",
            "need_request": ["full_info"],
            "tags": {
                "full_info": "encoded_tag"
            },
            "update_status": "stale"
        }
    ],
    "allowed_changes": [
        {
            "service": "taxi",
            "can_make_more_orders": true
        },
        {
            "service": "eats",
            "can_make_more_orders": false,
            "no_more_orders_reason": "reason"
        }
    ]
}
```

Поле `force` в запросе нужно для игнорирования на бекенде минимального времени жизни кеша (описано [здесь](#Недоступность-кеша) и [здесь](#Обновление-данных-заказа-пользователем)) Передаётся только после изменения заказа пользователем.

Интервал поллинга приходит с бека в заголовке `X-Yataxi-Polling-Interval-Ms` он может изменяться динамически, поэтому его нельзя кешировать. Фолбек на клиентах – 2 секунды.

Логика фонового полинга остаётся чисто клиентской.

Orders в ответе упорядочены.

### Поллинг taxiroute

Объект route является отдельным партом с типом поллинга `route_distance_depended` и типом парта `taxiroute`.

Ручка запроса такого типа парта принимает на вход

```json
{
    "coordinates": [
        37.67675076704057,
        55.681554945423315
    ],
    "timestamp": "2020-04-20T15:10:10+0300",
    "use_history": true
}
```

и возвращает ответ taxiroute.

### Получение дополнительных данных

Если хотя бы в одном заказе пришёл непустой массив `"need_request"`, то для таких заказов нужно сделать дополнительный запрос. Параметры запроса фиксируем на клиентах для `part_type`.

Для такси:

```json
{
    "extend_freecars": true,
    "format_currency": true,
    "supported": ["feature1", "featute2"],
    "position": {
        "point": [37.504381, 55.730800],
        "dx": 1009
    },
    "orders":[
        {
            "orderid":"order1",
            "tag": "encoded_part_tag"
        }
    ]
}
```

Это по сути то, что сейчас передаётся в `totw`.
Поле `"tag"` – тег из `tags`, который соответствует парту. В ответ тоже придёт поле `tag`, и в поллинг нужно будет подставить этот тег для парта.

В ответ для каждого заказа придёт часть полей из ответа `totw`. Для упрощения реализации на клиентах договариваемся, что режем ответ на разные ручки только по верхнему уровню json-а.

Ответ:

```json
{
    "orders": [
        {},{}
    ]
}
```

В случае ошибки запроса, нужно в интерфейсе для всех полей, ожидаемых в этом парте показать неактуальность данных.

## Особые случаи и их решение

### Версионирование объекта order_proc

Параметр `version` нужно добавить во все теги частей, которые отдают данные из order_proc.

Тег полученный от клиента нужно пробрасывать во все источники данных на случай, если от него зависит какая-то логика (как в примере с version).

Как минимум в первой версии тег нужно сделать совместимым с `version` чтобы при проксировании запроса в `order-core` можно было передать его или его часть в `order-info`.

### Опциональные поля

В totw сейчас есть некоторое количество полей, которые являются опциональными.

На клиентах нужно написать логику обработки ответа: если поле для парта есть в polling_policy, но не пришло в ответе, значит нужно удалить его во внутреннем представлении.

Для новых полей, которые добавляются в ответ ручки полинга, нужно либо делать их обязательными, либо предусматривать отдельное значение для обновления кеша и писать обработку этого на клиентах.

### Недоступность кеша

Может вызвать очень большую нагрузку на все сервисы, отдающие полную информацию о заказе.

У каждого тега в кеше должно быть минимальное время жизни: если оно не истекло, мы не просим клиента обновить данные и не проверяем совпадение тегов.
В нормальной ситуации это время может быть порядка нескольких секунд, однако в случае проблем с доступом к кешу, это время следует увеличить до значений порядка 10 секунд.
Тогда в худшем случае мы получим задержку получения полных данных на минимальное время жизни кеша и нагрузку на все сервисы на уровне текущей нагрузки для ручки `totw`.

### Недоступность источника заказов

В одном из этапов на бекенде нужно будет реализовать логику восстановления порядка заказов из лежащих сервисов по входным данным (`known_orders` в запросе).

Нужно в ответе восстановить порядок так, будто сервис работает (чтобы после поднятия сервиса не было перестановки заказов).

В случае недоступности одного из сервисов, нужно реализовать логику совмещения имеющегося порядка заказов на клиенте и порядка заказов от доступных сервисов. Для заказов, данные которых не получили от сервиса, значение `update_status` будет `stale` (чтобы клиент знал, когда показывать лоадер).

## Реализация тегов на бекенде

### Этап 1. Быстрое и простое решение

В первом этапе нужно сделать минимум: перейти на новое API, не ухудшив нагрузку на существующие сервисы.
А также отдавать вообще неизменяющиеся данные по заказу только в первом ответе.

Для реализации этого достаточно в качестве тега кеширования отдавать timestamp инвалидации данных.
Тогда в ответе `/mlutp/v1/orders/state` будет приходить, что нужно перезапросить `fast_info` не чаще, чем раз в 10 секунд (сейчас на iOS поллится раз в 5, на android раз в 10 секунд).
Неизменяемую информацию нужно вынести в отдельную ручку и отдавать необходимость её запросить только если объект `tags` вообще не пришёл в запросе на `launch` или `/mlutp/v1/orders/state`.

### Этап 2. Настоящее кеширование

Для реализации этого этапа нужно поднять redis.
В качестве ключа использовать `"{service_name}:{order_id}"`, значение – хеш-мап `tag_name->tag_value`.

Для упрощения работы с redis, нужно написать микросервис `order-tags`.
Микросервис должен реализовывать методы `get` `(order_id, service_nems) -> (tags)` и `set` `(order_id, service_name, tags)` - обновить переданные теги по заказу.

Поля в объекте заказа нужно разделить на группы и кешировать каждую группу независимо своим тегом.

Я выделил следующие группы:

- быстро отдающиеся важные поля `fast_fields`
- часто меняющиеся поля `often_changed_fields`
- редко меняющиеся поля `rarely_changed_fields`
- никогда не меняющиеся поля `never_changed_fields`
- очень медленно отдающиеся некритичные поля `slow_fields`
- имя фичи – если данные в ней меняются одновременно и объект фичи содержит много полей (>5), иначе экономии в посылаемых данных не будет.

Так как клиентское приложение будет уметь получать части информации о заказе из разных ручек, можно добавлять новые группы и переносить поля из группы в группу, инвалидировав все актуальные кеши.
Для инвалидации нужно сохранять версию разделения заказа на части на момент отдачи polling_policy.

Данные в redis добавляются при создании заказа, а так же в случае если при запросе тегов нет данных по заказу (могли удалиться по TTL).

## Изменение данных по фиче

После реализации [этапа 2](#Этап-2-Настоящее-кеширование) при изменении данных какой-либо фичи по заказу нужно изменить тег той части заказа, в которую входят изменённые поля фичи.

## Обновление данных заказа пользователем

Все обновления должны идти непосредственно в микросервис фичи, данные которой обновляются.
Микросервис фичи должен обновлять все теги, связанные с фичей при каждом изменении.

Механика восстановления порядка изменений и обработки гонок остаётся в ответственности микросервиса и зависит от кеширования.

Для того, чтобы получить данные по обновлённым тегам не дожидаясь минимального времени жизни кеша, нужно в запрос `/mlutp/v1/orders/state` добавить параметр `force=true`.
Однако, в случае недоступности кеша этот параметр будет игнорироваться чтобы обезопасить сервисы от нагрузки.

### Дальше описаны варианты как должно происходить взаимодействие с кешем для фич с разной логикой обработки клиентского апдейта

#### Версионирование данных по фиче

Данные фичи содержат версию. Клиент в запрос на обновление присылает последнюю известную ему версию данных.
Если версия актуальна, то происходит изменение данных, в ответ возвращается новая версия и UI оптимистично меняется в соответствии с запрошенным изменением, но блокируется до того, как в `/mlutp/v1/orders/state` по этой фиче придёт версия >= версии изменения.
Если версия не актуальна, то возвращается флаг ошибки и актуальный номер версии. UI оптимистично меняется и приложение ждёт, пока версия в orders/full станет >= актуальной на момент попытки апдейта, и повторяет запрос. Пока версия не актуальна, приложение присылает `force=true` в запросе `/mlutp/v1/orders/state`.

#### Восстановление порядка запросов на сервере

В этом варианте запросы на изменение должны быть идемпотентны и фича должна уметь восстановить хронологический порядок запросов на сервере. Тогда нам в принципе не важна последняя версия запроса на обновление, нам важно только определить последний во времени запрос (last wins). При любом обновлении тег меняется, и клиентское приложение должно оптимистично менять интерфейс и разблокировать его, когда в `/mlutp/v1/orders/state` придут данные, совпадающие с запросом на обновление (или послать retry обновления, если этого не произойдёт за N секунд). Здесь аналогично, пока не придёт ожидаемый апдейт в `/mlutp/v1/orders/state`, посылаем флаг `force=true`.

## Обратная совместимость

- Старая ручка totw будет ходить в те же микросервисы, что и новая. Когда-нибудь (2 года?) ее можно будет выключить

## Этапы разработки

### Этап 1

На клиентах:

1. начинаем парсить `polling_policy` и получать доп. информацию исходя из него,
1. делаем полинг новой ручки взамен старых + получаем дополнительные данные по тегам,
1. реализуем новый флоу частичного обновления данных о заказе,
1. рендерим заглушки под все заказы, которые пришли в ответе лонча сразу, не дожидаясь первого ответа полинга,
1. поддерживаем изменения в объекте driver (см. ниже),
1. для полинга `taxiroute` пока ничего не меняем, он работает по-старому.

На backend:

1. начинаем отдавать в `launch` правила `polling_policy`, в нём приходит два парта – текущий taxiroute и текущий totw,
1. добавляем ручку поллинга,
1. делаем вместо тега timestamp предыдущего ответа с need_request этого парта,
1. `version` `order_proc`'а пока оставляем параметром запроса парта `"part_type":"totw"`,
1. распиливаем объект `driver` из ответа `totw` на два, чтобы не было часто и редко меняющихся данных в одном вложенном объекте (или выпиливаем из driver часто меняющиеся данные за ненадобностью).

### Этап 2

На backend:

1. для такси выделяем 2 группы:
    1. `fast_fields` – всё, что сейчас в totw,
    1. `never_changed_fields` – route_sharing_url, currency_rules, может ещё что-то,
1. добавляем ручки запроса полной информации (проксируем в существующие сервисы).

На клиентах:

1. для полинга taxiroute берём url из правил поллинга.

### Этап 3

На backend:

1. Добавляем парт `slow_fields` – `orderperformerinfo`,
1. выкидываем из ответов ручек с полной информацией о заказе поля, которые не используются на свежих клиентах.

Backend + клиенты:

1. добавляем в схему `orderchat` + `chathistory`,
1. Либо на iOs делаем кеширование стейта заказов между запусками приложения, либо на бекенде в лонче начинаем отдавать больше информации о заказах (по `"extended_order_info" in supported`).
1. В информации о заказе в `launch` присылать не только статус, но большее количество данных о заказе для частичного рендеринга
1. На клиентах частично рендерить заказы после ответа `launch`.

### Этап 4 (вне проекта мультизаказа)

На backend:

1. делим ответ totw на большие части по разным сервисам и начинаем кешировать через распределённый кеш.

На backend и клиентах:

1. в ответ `/mlutp/v1/orders/state` по каждому заказу добавляем информацию о возможностях его изменения.
