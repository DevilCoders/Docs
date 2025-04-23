## TurnOnAutopayJob

### Продукт/подсистема

Оплата, пополнение счета.


### Роль в работе продукта/подсистемы

Включает клиенту автоплатёж после привязки карты.


### Датафлоу

- Достает задания на включение автоплатежа из очереди [dbqueue](https://direct-dev.yandex-team.ru/db/ppc/tables/dbqueue_jobs.html) (тип задания `turn_on_autopay`).
- Обращается в Биллинг по API для проверки воможности включить автоплатёж.
- По возможности включает автоплатёж в настройках кампании-кошелька в MySQL.


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.TurnOnAutopayJob.working.production&query=&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'payment.TurnOnAutopayJob)~limit~100~offset~0~reverseOrder~true~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы

Перестанет включаться автоплатёж.


### Как пользователи (или команда) заметят проблему и через какое время

?


### Контакты разработчиков и менеджеров

Разработчики: [Александр Дуплищев](https://staff.yandex-team.ru/ppalex)


### Желательное время исправления в случае поломки

В течение суток.


### Способы регулирования работы джобы

Отсутствуют.


### Известные причины поломок

Отсутствуют.


### Дополнительно: тонкости и подводные камни
