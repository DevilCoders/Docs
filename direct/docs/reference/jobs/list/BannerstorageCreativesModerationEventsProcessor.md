## BannerstorageCreativesModerationEventsProcessor

### Продукт/подсистема

Модерация performance-креативов (продукт, известный иначе как "смарт-баннер").


### Роль в работе продукта/подсистемы

Отправляет креативы в Модерацию.


### Датафлоу

Почти классический модерационный ESS-процессор, только ходит еще в BannerStorage.

- Отслеживает изменения в креативах, таблица [perf_creatives](https://direct-dev.yandex-team.ru/db/ppc/tables/perf_creatives.html).
- Читает актуальные данные по креативам из MySQL.
- Выполняет запрос в API BannerStorage за дополнительной информацией.
- Мёржит информацию.
- Выполняет запрос в API BannerStorage для изменения статуса креатива на "Ожидает модерации".
- Отправляет заявку в Модерацию через LogBroker.


### Способы наблюдения за текущим состоянием

- [График отставания](https://solomon.yandex-team.ru/?project=direct&cluster=app_java-jobs&service=java-monitoring&l.host=CLUSTER&l.sensor=binlog_delay&l.shard=*&graph=auto&l.ess_processor=export_moderation_bannerstorage_creatives_moderation&b=1h&e=)
- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.BannerstorageCreativesModerationEventsProcessor.working.production&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'bannerstorage.BannerstorageCreativesModerationEventsProcessor)~limit~100~offset~0~reverseOrder~true~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы

Не будут отправляться креативы в Модерацию (критично)


### Как пользователи (или команда) заметят проблему и через какое время

Через несколько часов осознают, что креативы так и не были промодерированы, могут начать жаловаться.


### Контакты разработчиков и менеджеров

Разработчики: [Игорь Костромин](https://staff.yandex-team.ru/elwood), [Алексей Кашицын](https://staff.yandex-team.ru/aliho)

### Желательное время исправления в случае поломки

Как можно раньше.


### Способы регулирования работы джобы

- [Общие способы регулирования работы ESS-процессоров](../jobs-common.md#control-ess)


### Известные причины поломок

BannerStorage API не работает
lbkx не работает


### Дополнительно: тонкости и подводные камни
