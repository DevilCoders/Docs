# Использование juggler-алертов

## Добавление проверки

Juggler-проверки можно генерить на основе данных из [Prometheus](prometheus.md) и [Solomon](solomon.md).

Для того чтобы добавить алерт нужно:
- Добавить в BUILD файл вашего сервиса рулы `prometheus_alert` или `solomon_alert`.
- Выполните `make alerts` и закоммитьте все измененные файлы.
- Через некоторое время после мержа в trunk алерты появятся в juggler.

## Как найти свои проверки в juggler
- можно фильтровать по указанному вами тегу с префиксом **vertis_ops_** для прода и **vertis_ops_test_** для тестинга ([пример][1])
- все проверки для сервиса можно найти по хосту, который равен имени сервиса для прода или имени сервиса с префиксом **test_** для тестинга ([пример][2])
- конкретную проверку можно найти по имени алерта (alert_name) ([пример][3]), а если нужна проверка только для прода, можно [добавить][4] в условие хост

## Как настроить уведомления в telegram
Для получения уведомлений в telegram, нужно сначала зарегистрировать чат или человека по [инструкции](https://docs.yandex-team.ru/juggler/notifications/on_change#telegram).  
Затем нужно создать notification rule, опять же отфильтровав нужные алерты одним из указанных выше способов.  
Пример notification rule:
```
project: vertis-ops
selector: tag=vertis_ops_doppel
template_name: on_status_change
match_raw_events: false
template_kwargs:
    status:
        - OK
        - CRIT
    login:
        - vertis-projects-alerts
        - some-login
    method:
        - telegram
    day_start: 1 # если не нужно отправлять уведомления, например, по выходным. Не указывать, если нужно отправлять всегда
    day_end: 5
    time_start: '11:00' # аналогично, ограничение отправки по времени суток
    time_end: '22:00'
    repeat: 3600 # если нужно отправлять уведомление повторно, период в секундах
check_kwargs: {}
description: ''
```

Помимо ограничений на уведомлений по дням недели и времени суток можно настраивать [мьюты][7].  
Например, если по поводу горящей проверки уже есть тикет, можно указать startrek_ticket, и мьют автоматически завершится, когда этот тикет будет закрыт (для этого надо выдать **robot-juggling** доступ на просмотр вашей очереди).

[Больше примеров][6]  

Про другие доступные опции, например, звонки от железной тётки, можно почитать в [документации][5] juggler.  

[1]: https://juggler.yandex-team.ru/aggregate_checks/?project=vertis-ops&query=tag%3Dvertis_ops_auto_c2b
[2]: https://juggler.yandex-team.ru/aggregate_checks/?project=vertis-ops&query=host%3Dtest_doppel-yt-controller
[3]: https://juggler.yandex-team.ru/aggregate_checks/?project=vertis-ops&query=service%3Ddoppel-yt-controller_unexpected_restart
[4]: https://juggler.yandex-team.ru/aggregate_checks/?project=vertis-ops&query=service%3Ddoppel-yt-controller_unexpected_restart%26host%3Ddoppel-yt-controller
[5]: https://docs.yandex-team.ru/juggler/notifications/on_change
[6]: https://juggler.yandex-team.ru/notification_rules?project=vertis-ops
[7]: https://docs.yandex-team.ru/juggler/notifications/mutes
