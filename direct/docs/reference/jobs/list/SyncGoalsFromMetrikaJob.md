### SyncGoalsFromMetrikaJob

### Продукт/подсистема

Центр конверсий

### Роль в работе продукта/подсистемы

На момент создания источника конверсии, цели в метрике (в которые загружается через CRM API)
могут быть не созданы. Цели создаются после загрузки конверсий в CRM API, создаются с определёнными типами. По этим
типам мы их определяем и подгружаем в Директ.

### Датафлоу

- Достаём из базы источники конверсий, в которых не указана цель в конверсионных действиях, но уже прошла обработка и
  она успешно завершилась
- По счётчикам из этих источников конверсий достаём цели в метрике определённых типов
- Обновляем источники конверсий в базе, указывая цели в конверсионных действиях

### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.SyncGoalsFromMetrikaJob.working.production&query=&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'conversionsource.SyncGoalsFromMetrikaJob)~limit~100~offset~0~reverseOrder~true~showTraceIdRelated~false))$)

### Как пользователи (или команда) заметят проблему и через какое время

Без подтягивания целей не будет видна статистика достижений

### Контакты разработчиков и менеджеров

Разработчики: [Захар Зибаров](https://staff.yandex-team.ru/zakhar) <br/>
Менеджеры: [Антон Огай](https://staff.yandex-team.ru/aogay)

### Желательное время исправления в случае поломки

В течение суток
