## CheckedSupportChatSyncJob

### Продукт/подсистема

Чат поддержки в гридах.


### Роль в работе продукта/подсистемы

У некоторых клиентов не должно быть доступа к чату. Джоба управляет доступом к чату поддержки через синхронизацию со списком исключений в YT, составленным группой продаж среднему и малому бизнесу (SMB).

Джоба включает или выключает доступ к фиче `checked_support_chat`, сравнивая состояние фичи в выгрузке БД в YT и таблицы от SMB. Выключает всем указанным в таблице, включает, если фича у клиента выключена, а в таблице клиента нет. Сама фича раскатана на 100%.


### Датафлоу

- Каждые полчаса строим дифф между [hahn.//home/oobp/public/clients_chat_exclusion](https://yt.yandex-team.ru/hahn/navigation?path=//home/oobp/public/clients_chat_exclusion) (клиенты, у которых должна быть отключена фича) и  [ppc.clients_features](https://direct-dev.yandex-team.ru/db/ppc/tables/clients_features.html) со всех шардов (клиенты, у которых отключена фича).
- Получаем списки на включение и отключение.
- Делаем запросы в ppc на изменение фичи `checked_support_chat`.
- Пишем в проперти `CHECKED_SUPPORT_CHAT_FEATURE_LAST_SYNCED_MOD_TIME` время модификации таблицы из YT.


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.CheckedSupportChatSyncJob.working.production&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(method~'featuresync.CheckedSupportChatSyncJob)~limit~100~offset~200~reverseOrder~false~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы

Кому-то захотят вернуть чат (вместо общения почтой с менеджером), а он его не получит. И наоборот.


### Как пользователи (или команда) заметят проблему и через какое время

Однажды поломали на три недели в обход мониторинга, починили, когда просто смотрели код по случаю.
Так иногда пользователи жалуются на отсутствие чата поддержки, только обычно это не от джобы.


### Контакты разработчиков и менеджеров

Разработчики: [Кирилл Богданов](https://staff.yandex-team.ru/sco76), [Роман Кухта](https://staff.yandex-team.ru/kuhtich) <br/>
Менеджеры в Директе: [Александр Липчин](https://staff.yandex-team.ru/lipchin), [Дмитрий Суворов](https://staff.yandex-team.ru/dmsuvorov)
Менеджеры: [Дмитрий Кудинов](https://staff.yandex-team.ru/dimaku), [Елена Кутепова](https://staff.yandex-team.ru/lenakut)


### Желательное время исправления в случае поломки

Неделя.


### Способы регулирования работы джобы

- `CHECKED_SUPPORT_CHAT_FEATURE_LAST_SYNCED_MOD_TIME` - можно отключить джобу, поставив время из будущего.


### Известные причины поломок

- Таблицу в YT могут потерять.
- Потенциально может несколько раз подряд не отрабатывать запрос в YT.


### Дополнительно: тонкости и подводные камни

