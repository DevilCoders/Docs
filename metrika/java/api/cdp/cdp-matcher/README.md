# CDP-MATCHER
Matcher (не смог придумать русского слова) идентификаторов клиентов в CDP и идентификаторов посетителей в Яндекс.Метрике.
Описание CDP можно прочитать тут - https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/README.md

## Описание
`cdp-matcher` - процессинговый сервис, отвечающий за сопоставление идентификаторов клиентов в CDP (`cdp_uid`) и
идентификаторов посетителей в Яндекс.Метрике (`user_id`). Сопоставление происходит с помощью промежуточного идентификатора
(`client_id` или `FirstPartyCookie` в логах метрики). Данные о полученных сопоставлениях используются
в `cdp-ch-writer` ([описание](https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/cdp-ch-writer/README.md)) и
в `cdp-orders-exporter` ([описание](https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/cdp-orders-exporter/README.md))

### Deployment
production - https://deploy.yandex-team.ru/stages/cdp-matcher-production

testing - https://deploy.yandex-team.ru/stages/cdp-matcher-test

### Какие данные потребляет?
`cdp-matcher` читает информацию для сопоставления идентификаторов, которые пишут два сервиса
`cdp-core` ([описание](https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/cdp-core/README.md)) и
`cdp-filter` ([описание](https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/cdp-filter/README.md))
 из двух консюмеров
в Logbroker:
1. Консюмер, из которого читаются данные о `user_id` - `metrika-client-id-add-consumer` (`message MetrikaClientIdAdd`)
2. Консюмер, из которого читаются данные о `cdp_uid` - `cdp-client-id-change-consumer` (`message CdpClientIdChange`)

Данные едут в формате protobuf - [схема тут](https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/cdp-processing-common/proto/matching.proto)

### Как обрабатывает данные?
`cdp-matcher` по сути своей весьма прямая реализация джойна двух логов в realtime, слегка приправленная бизнес логикой.
Мы хотим приджойнить к `cdp_uid` нужные `user_id` по `client_id`. Одной из сложностей этого процесса является то, что и
соответствия между `cdp_uid` и `client_id` и соответствия между `user_id` и `client_id` - это многие ко многим, и с этим
приходится как-то работать.

Везде далее, я буду опускать упоминание счётчика, но важно помнить что джойн данных всегда происходит по данным внутри счётчика,
то есть:
1. `counter_id` всегда является частью ключа всех таблиц
2. все данные в логах содержат конкретный `counter_id`
3. соответствия мы ищем тоже в рамках одного `counter_id`

И так, есть 4 таблицы в YDB, в которых хранится текущее состояние:
1. `matching/client_client_id` - маппинг из `cdp_uid` в `client_id` (`cdp_uid -> client_id`).
2. `matching/client_id_client` - `client_id -> cdp_uid`
3. `matching/client_id_user_id` - `client_id -> user_id`
4. `matching/client_user_id` - `cdp_uid -> user_id`. Эта таблица, по сути, является результатом работы `cdp-methcer`. Она
и есть то самое соответствие, которые мы тут строим, и состояние, консистентность которого поддерживаем.

Изначально все 4 таблицы пустые.

#### Транзакционность
Перед тем как рассуждать о конкретных алгоритмах обработки данных, стоит отметить, что это место одно из достаточно сильно
нагруженных в системе в целом, что требует парализации обработки, что потенциально может приводить к конкурентной работе
с данными (например data race). Чтобы избежать проблем с консистентностью данных при таких условиях, используются транзакции
на уровне базы данных YDB для изоляции изменений друг от друга. Про транзакции в YDB можно прочитать в
[документации](https://ydb.yandex-team.ru/docs/concepts/transactions# rezhimy-tranzakcij).

#### Данные о `user_id`
Когда к нам приезжает информация (из логов метрики) об очередной паре `(user_id, client_id)` мы делаем следующее:
1. Проверяем если такая пара уже у нас в таблице `matching/client_id_user_id`. Если есть, то не обрабатываем её, так как
уже раньше она встречалась. Если нет, то сохраняем её в таблицу `matching/client_id_user_id` и продолжаем обработку.
2. Достаём из `matching/client_id_client` маппинг `client_id -> cdp_uid` (их может быть несколько)
3. Для всех `cdp_uid` добавляем пары `cdp_uid -> user_id` в таблицу `matching/client_user_id`. Кроме этого запоминаем те
`cdp_uid`, для которых поменялся их набор `user_id`, чтобы потом отправить записать информацию об этом в Logbroker.

Обработка данных о `user_id` более простая и эффективная, так как пары `(user_id, client_id)` по сути своей append only,
в том смысле, что если однажды была замечена такая пара, то она уже не может пропасть. При описанной выше схеме обработки
мы на самом деле можем посчитать что к `cdp_uid` добавился какой-то `user_id`, хотя на самом деле этого не происходило и
данный `user_id` уже был привязан к этому `cdp_uid`, просто через другой `client_id`, но это не критично, так как в целом
набор `user_id` для данного `cdp_uid` дедублицируется на уровне базы. С другой стороны такой подход позволяет игнорировать
уже описанное выше отношение многие к многим в момент джойна и экономить походы в базу, не стоя полный граф связей идентификаторов
`user_id -> client_id -> cdp_uid`.

#### Данные о `cdp_uid`
Данные о `cdp_uid` имеют более сложный формат и (опуская упоминания `counter_id`) выглядят как тройка `(cdp_uid, client_id, action)`,
где `action` - это либо `add`, либо `remove`. Эти данные, в отличие от данных по `user_id`, как видно из формата, свойством
append only уже не обладают и тут уже прийдётся по-честному считаться с тем что связь между идентификаторами это многие
ко многим и строить полноценный граф связи идентификаторов. Для описания процесса обработки таких данных рассмотрим пример:
Пусть изначально для выбранного `cdp_uid` есть следующие соответствия:
```
cdp_uid -> client_id_1
cdp_uid -> client_id_2
cdp_uid -> client_id_3
```

Для `client_id` существуют свои соответствия:
```
client_id_1 -> user_id_1
client_id_1 -> user_id_2
client_id_2 -> user_id_2
client_id_2 -> user_id_3
client_id_3 -> user_id_4
client_id_3 -> user_id_5
client_id_4 -> user_id_5
```

Из этого можно построить граф
```
           --> client_id_1 ---> user_id_1
          /               \
         /                 ---> user_id_2
        /                 /
cdp_uid -----> client_id_2 ---> user_id_3
        \
         ----> client_id_3 ---> user_id_4
                          \
                           ---> user_id_5
```

Из этого графа можно видеть что при таком состоянии `cdp_uid` соответствует набор из `[user_id_1, user_id_2, user_id_3, user_id_4, user_id_5]`.
Предположим что пришло 2 сообщения:
```
cdp_uid, client_id_1, remove
cdp_uid, client_id_4, add
```

Для получения нового состояния нужно из графа привязок удалить ребра соответствующие `remove` и добавить ребра соответствующие `add`.
После этого получится вот такой граф:
```
                           ---> user_id_2
                          /
cdp_uid -----> client_id_2 ---> user_id_3
        \
         ----> client_id_3 ---> user_id_4
         \                 \
          \                 --> user_id_5
           \               /
            -> client_id_4
```

После обновления `cdp_uid` соответствует набор из `[user_id_2, user_id_3, user_id_4, user_id_5]`. На этом примере легко
заметить, что добавление `client_id` не обязательно приводит к добавлению `user_id`, а удаление `client_id` не обязательно
приводит к удалению всех связанных с ним `user_id`.

Таким образом обновление данных, при получении тройки `(cdp_uid, client_id, action)`, сводится к :
1. Чтению данных из таблиц `matching/client_client_id` и `matching/client_id_user_id` для получения текущего графа связей
для данного `cdp_uid`
2. Чтению из `matching/client_id_user_id` данных о соответствиях между данным `client_id` и записанными ранее в базу `user_id`.
3. Модификация графа, в соответствие с полученным `action`.
4. Сохранение (добавление или удаление) в таблицы `matching/client_client_id` и `matching/client_id_client` информации
об изменении соответствий `cdp_uid -> client_id` в соответствии с полученным `action`.
5. Сохранение (добавление или удаление) в таблицу `matching/client_user_id` информации об изменении соответствий `cdp_uid -> user_id`
в соответствии с изменениями в графе.

#### Шардирование
Так как джойн происходит по client_id обработка пошардированна (на уровне партиций в Logbroker и на уровне таблиц в YDB, если это возможно),
по непрерывным отрезкам значений `int64Hash(client_id)`. Это позволяет равномерно распределять нагрузку между шардами обработки
и максимизировать локальность данных в смысле количества затронутых в одной транзакции шардов талицы в YDB.


### Куда пишет данные?
Как уже было сказано раньше, результирующие данные хранятся в таблице `matching/client_user_id` в YDB. Помимо этого ключи
клиентов, для которых изменился маппинг `cdp_uid -> user_id` пишутся в топик `updated-clients-topic`. Данные едут в формате
protobuf - [схема тут](https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/cdp-common/proto/cdp.proto) (`message ClientKey`).


## Графики
Графики для production:
1. [Мониторинг консюмера `metrika-client-id-add-consumer` в Logbroker](https://logbroker.yandex-team.ru/lbkx/accounts/metrika/prod/cdp/metrika-client-id-add-consumer)
2. [Мониторинг консюмера `cdp-client-id-change-consumer` в Logbroker](https://logbroker.yandex-team.ru/lbkx/accounts/metrika/prod/cdp/cdp-client-id-change-consumer)
3. [Мониторинг топика `updated-clients-topic` в Logbroker](https://logbroker.yandex-team.ru/lbkx/accounts/metrika/prod/cdp/updated-clients-topic)
