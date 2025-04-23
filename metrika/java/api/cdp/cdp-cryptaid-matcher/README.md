# CDP-CRYPTAID-MATCHER
Matcher (не смог придумать русского слова) идентификаторов клиентов в CDP и идентификаторов профиля пользователя в Крипте.
Описание CDP можно прочитать тут - https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/README.md

## Описание
`cdp-cryptaid-matcher` - процессинговый сервис, отвечающий за сопоставление идентификаторов клиентов в CDP (`cdp_uid`) и
идентификаторов профиля пользователя в Крипте (`crypta_id` и `glued_yuid`). Сопоставление происходит с помощью
информации о email-ов и телефонов клиента в CDP. Данные о полученных сопоставлениях используются
в `cdp-ch-writer` ([описание](https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/cdp-ch-writer/README.md)) и
в `cdp-orders-exporter` ([описание](https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/cdp-orders-exporter/README.md))

### Deployment
production - https://deploy.yandex-team.ru/stages/cdp-cryptaid-matcher-production

testing - https://deploy.yandex-team.ru/stages/cdp-cryptaid-matcher-test

### Какие данные потребляет?
`cdp-cryptaid-matcher` читает ключи клиентов в CDP, которые пишут два сервис
`cdp-core` ([описание](https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/cdp-core/README.md)) и
`cdp-scheduler` ([описание](https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/cdp-scheduler/README.md))
 из консюмера `changed-emails-and-phones-consumer` в Logbroker  (`message ClientKey`).

Данные едут в формате protobuf - [схема тут](https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/cdp-common/proto/cdp.proto)

### Как обрабатывает данные?
При получении очередного ключа клиента `cdp-cryptaid-matcher` выполняет следующие действия:
1. Читает из таблицы `clients_data/clients` информацию о email-ax и телефонах данного клиента (в том числе и о хэшированных).
2. Для каждого прочитанного идентификатора делается запрос в BigB для получения набора идентификаторов: `crypta_id` и `glued_uid`.
В общем конкретному клиенту может соответствовать несколько `crypta_id`, но по факту кейс достаточно редкий.
3. Полученные данные об идентификаторах сохраняются в таблицы `matching/client_crypta_id` и `matching/client_glued_yuid`
в YDB и так же проверяется изменился ли набор идентификаторов для данного клиента. Если да, его ключ запоминается для того,
чтобы отправить "дальше по трубам" информацию об обновлении данных.


### Куда пишет данные?
Как уже было сказано раньше, результирующие данные хранятся в таблицах `matching/client_crypta_id` и `matching/client_glued_yuid`
в YDB. Помимо этого ключи клиентов, для которых изменился набор идентификаторов  `crypta_id` или `glued_uid` пишутся
в топик `updated-clients-topic`. Данные едут в формате protobuf -
[схема тут](https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/cdp-common/proto/cdp.proto) (`message ClientKey`).


## Графики
Графики для production:
1. [Мониторинг консюмера `changed-emails-and-phones-consumer` в Logbroker](https://logbroker.yandex-team.ru/lbkx/accounts/metrika/prod/cdp/changed-emails-and-phones-consumer)
2. [Мониторинг топика `updated-clients-topic` в Logbroker](https://logbroker.yandex-team.ru/lbkx/accounts/metrika/prod/cdp/updated-clients-topic)
