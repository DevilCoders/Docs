## NotifyClientCashbackJob

### Продукт/подсистема

Программа лояльности пользователей — начисление пользователям кешбэков за использование определённой функциональности в Директе.

### Роль в работе продукта/подсистемы

Отправка писем о бонусах, начисленных за прошлый месяц, по всем аккаунтам пользователя.

### Датафлоу

- Проверяем наличие необработанных табличек
- По чанкам читаем табличку
- Для каждого чанка делаем отправку через платформу коммуникации

При падения следующий запуск начнет исполнения с чанка, на котором упали.

### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.NotifyClientCashbackJob.working.production)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'cashback.NotifyClientCashbackJob)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)

### Какая функциональность пострадает от отказа джобы

Перестанем рассылать письма о бонусах

### Как пользователи (или команда) заметят проблему и через какое время?

После очередного начисления бонусов (обычно в начале месяца)

### Контакты разработчиков и менеджеров

Разработчик: [Саша Дубов](https://staff.yandex-team.ru/a-dubov) <br/>
Менеджер: [Ярослав Михайлов](https://staff.yandex-team.ru/yarmikh)

### Желательное время исправления в случае поломки

До очередного начисления бонусов. Обычно в начале каждого месяца. Уточнить следует через менеджеров.

### Способы регулирования работы джобы

- ppc-property `notify_cashback_cluster` - кластер с данными
- ppc-property `notify_cashback_directory` - директория, в которой проверяем таблички
- ppc-property `notify_cashback_table_creation_time` - время создания последней обработанной таблички в формате YT (например, 2022-06-30T14:33:35.605468Z)
- ppc-property `notify_cashback_row_number` - последняя обработанная строка в таблице
- ppc-property `notify_cashback_chunk_size` - размер чанка

### Известные причины поломок

- невалидные данные в табличке
