## ClientsFeaturesChangesLogJob

### Продукт/подсистема

Feature-флаги (aka фичи).


### Роль в работе продукта/подсистемы

Джоба записывает в тикет на фичу события привязки/отвязки клиентов. Суть джобы в том, что она помогает ответственному за фичу отслеживать такие события.


### Датафлоу

- читает события из ClickHouse из таблицы `binlog_rows_v2` (для таблицы [ppc.clients_features](https://direct-dev.yandex-team.ru/db/ppc/tables/clients_features.html));
- читает так же дополнительные данные из MySQL;
- затем записывает изменения в специальный тикет в стартреке (прописанный в `ppcdict.features.ticket_id`).


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.ClientsFeaturesChangesLogJob.working.production&query=&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'featureschanges.ClientsFeaturesChangesLogJob)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы

В тикеты перестанут записываться события привязки/отвязки фич клиентам.


### Как пользователи (или команда) заметят проблему и через какое время

Ответственные за фичи перестанут получать информацию об изменениях в фичах, сами могут этого не заметить.


### Контакты разработчиков и менеджеров

Разработчики: [Белоусов Сергей](https://staff.yandex-team.ru/mexicano)


### Желательное время исправления в случае поломки

В течение недели.


### Способы регулирования работы джобы

- `features_bin_logs_reader.clients_features_ignored_features_ids`. Содержит идентификаторы фич (Primary Key), для которых не нужно писать события в тикет. Полезно для игнорирования фич, которые выдаются клиентам массово из кода.


### Известные причины поломок

- Проблемы с трекером.
- Если появляется новая фича, которая используются нестандартным способом - выдаётся массово клиентам из кода напрямую, а не через процент, - то в тикете очень быстро достигается лимит сообщений 1К. Для исправления используйте проперти `features_bin_logs_reader.clients_features_ignored_features_ids` (описание выше).
- Если событий слишком много и джоба ClientsFeaturesChangesLogJob не будет успевать их обрабатывать, то загорится CRIT в джаглере (сейчас разрешено отставать не более чем на 1 час).

### Дополнительно: тонкости и подводные камни

Если `FeaturesHistoryChangesLogJob` по какой-то причине пропустит событие создания фичи и не создаст тикет, то `ClientFeaturesChangesJob` будет ждать, пока не появится тикет и перестанет делать полезную работу (зациклится). Для решения проблемы нужно будет создать тикет и прописать его в `ppcdict.features.ticket_id` с помощью ваншота [CreateFeaturesTicketsOneshot](https://a.yandex-team.ru/arc/trunk/arcadia/direct/oneshot/src/main/java/ru/yandex/direct/oneshot/oneshots/featurestickets/CreateFeaturesTicketsOneshot.java).

Скрипт [update_features_history.py](https://a.yandex-team.ru/arc/trunk/arcadia/direct/perl/python/scripts/update_features_history.py), пишущий `features_history`, может сломаться. Джоба `FeaturesHistoryChangesLogJob` зависит от этого скрипта, и она создаёт тикеты на фичи. Если джоба `ClientsFeaturesChangesLogJob` увидит событие привязки фичи к клиенту, а джоба `FeaturesHistoryChangesLogJob` еще не создала к этому времени тикет, то `ClientsFeaturesChangesLogJob` будет ждать, пока тикет не будет создан. Через час отставания juggler-проверка перейдет в CRIT.
