## StoredVarsCleaner

### Продукт/подсистема

Excel, Медиапланы.


### Роль в работе продукта/подсистемы

Очистка таблицы для храненния сессионных данных [monitor.stored_vars](https://direct-dev.yandex-team.ru/db/monitor/tables/stored_vars.html) от старых значений.


### Датафлоу

Ищет в таблице stored_vars в базе monitor значенения старше 7 дней и удаляет их


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.StoredVarsCleaner.working.production&query=&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(method~'sessionvariables.StoredVarsCleaner~service~'direct.jobs)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы

Таблица [monitor.stored_vars](https://direct-dev.yandex-team.ru/db/monitor/tables/stored_vars.html) имеет свойство неограниченно увеличиваться в размерах. Если очистка прекратится, то в худшем случае у нас когда-нибудь кончится место в базе monitor. Также очищаемая этой джобой таблица используется в perl при импорте кампаний и медиапланов через Excel-файлы. Возможно замедление работы/500-ки, если таблица будет слишком большой.


### Как пользователи (или команда) заметят проблему и через какое время

(Теоретически) Проблемы с импортом кампаний и медиапланов через Excel-файлы


### Контакты разработчиков и менеджеров

Разработчики: [Сергей Гукасьян](https://staff.yandex-team.ru/gukserg)


### Желательное время исправления в случае поломки

Неделя+.


### Способы регулирования работы джобы

-


### Известные причины поломок

-


### Дополнительно: тонкости и подводные камни
