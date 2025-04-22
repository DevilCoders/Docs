## ClientAvatarsDeleteJob

### Продукт/подсистема

Хранение аватарок клиентов. На момент написания (5.04.2021) доступно только фрилансерам.


### Роль в работе продукта/подсистемы

Удаляет неиспользуемые аватарки из аватарницы (mds) и записи о них в Директе.


### Датафлоу

- Находит неиспользуемые аватарки в реестре аватарок [ppc.clients_avatars](https://direct-dev.yandex-team.ru/db/ppc/tables/clients_avatars.html) (проверяя связь с фрилансерами).
- Помечает их удалёнными (`ppc.clients_avatars.is_deleted`).
- Удаляет их из Аватарницы.
- Удаляет записи о них из MySQL.


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.ClientAvatarsDeleteJob.working.production&last=1DAY&query=)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'gc.ClientAvatarsDeleteJob)~limit~100~offset~0~reverseOrder~true~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы

Будут накапливаться неиспользуемые аватарки в mds и MySQL.


### Как пользователи (или команда) заметят проблему и через какое время

Пользователи не заметят.


### Контакты разработчиков и менеджеров

Разработчики: [Игорь Гердлер](https://staff.yandex-team.ru/gerdler)


### Желательное время исправления в случае поломки

Неделя+.


### Способы регулирования работы джобы

- Ppc-property `clients_avatars_deletion_enabled` - включает/выключает джобу.


### Известные причины поломок

-


### Дополнительно: тонкости и подводные камни
