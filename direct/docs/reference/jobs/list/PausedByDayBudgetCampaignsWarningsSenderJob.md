## PausedByDayBudgetCampaignsWarningsSenderJob

### Продукт/подсистема

Система уведомлений клиента о событиях

### Роль в работе продукта/подсистемы

Отправляет письма об остановке кампании по достижению дневного бюджета.
Складывает такие события в **Eventlog**.

### Датафлоу

Джоба делает вычисления на базе **ppc** по таблицам **campaigns** и **camp_options**,
обновляет статус отправки уведомления в **ppc.camp_options**,
делает отправку писем через **Рассылятор**,
делает запись в **ppc.eventlog**.

### Способы наблюдения за текущим состоянием

[Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.PausedByDayBudgetCampaignsWarningsSenderJob.working.production&project=direct.prod&sort=DEFAULT&query=&last=1DAY)

[Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(from~'20211125T144204~to~'20211125T235959~fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(method~'daybudget.PausedByDayBudgetCampaignsWarningsSenderJob)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)
А также бинлоги по таблицам **ppc.camp_options** и **ppc.eventlog** метода *daybudget.PausedByDayBudgetCampaignsWarningsSenderJob*.

### Какая функциональность пострадает от отказа джобы

Не будут ходить уведомления пользователю об остановке кампаний по достижению дневного бюджета.
Не будет складываться событие в лог событий, доступный по публичному API.

### Как пользователи (или команда) заметят проблему и через какое время

Через день-два начнут появляться запросы в поддержку от пользователей.

### Контакты разработчиков и менеджеров

Разработчик: [Кирилл Богданов](https://staff.yandex-team.ru/sco76)
Менеджер: [Ярослав Михайлов](https://staff.yandex-team.ru/yarmikh)

### Желательное время исправления в случае поломки

В течение недели

### Способы регулирования работы джобы

Можно переключить клиента на старый контур уведомлений,
отключив фичу *paused_by_day_budget_warnings* —
это также отключит обработку в PausedByDayBudgetWalletsWarningsSenderJob

### Известные причины поломок

### Дополнительно: тонкости и подводные камни
