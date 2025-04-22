### Продукт/подсистема

Товарная реклама(Смарты, ДО, Фиды в ТГО).

### Роль в работе продукта/подсистемы

Проставляет статус "выключен" для фидов, которые давно не использовались в Директе, чтобы MBI передал этот статус в DataCamp, и офферы удалились

### Датафлоу

Достает из MySQL фиды, которые были помечены неиспользуемыми в период от "предыдущий запуск джобы минус 2 недели" до "сейчас минус 2 недели"<br />
Дергает ручки MBI для выключения этих фидов (пока что ручки не батчевые).

### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&last=1DAY&service=jobs.DisableFeedsInMBIJob.working.production)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'feed.DisableFeedsInMBIJob)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)

### Какая функциональность пострадает от отказа джобы

Невыключение фидов может со временем повлечь за собой рост объема данных в DataCamp и общей нагрузки на инфру Маркета

### Как пользователи (или команда) заметят проблему и через какое время

Пользователи не заметят никак.

### Контакты разработчиков и менеджеров

Разработчики: [buhter](https://staff.yandex-team.ru/buhter) <br/>
Менеджеры: [ulyashevda](https://staff.yandex-team.ru/ulyashevda)

### Желательное время исправления в случае поломки

Неделя
