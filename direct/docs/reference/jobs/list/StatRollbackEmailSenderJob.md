## StatRollbackEmailSenderJob
### Продукт/подсистема
Отправка пользователям писем об откатах статистики в кампаниях


### Роль в работе продукта/подсистемы
Отправляет пользователю письмо с сообщением о том, что ему на Общий счет или кампанию вернулись деньги за недействительные клики и/или конверсии.
Джоба заменяет письма клиентам, отправляемые скриптом [ppcStatRollbackNotify](https://a.yandex-team.ru/arc/trunk/arcadia/direct/perl/protected/ppcStatRollbackNotify.pl)



### Датафлоу
- Получает записи из таблицы [ppc.stat_rollback_data](https://direct-dev.yandex-team.ru/db/ppc/tables/stat_rollback_data.html).
- Выбирает дополнительные данные о пользователе и наличии у него Общего счета.
- Вычисляет подстановочные параметры и отправляет письма через Рассылятор.
- После отправки письма (или если рассылятор ответил что email невалидный) - удаляем запись из таблицы ppc.stat_rollback_data.



### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.StatRollbackEmailSenderJob.working.production&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'rollbacknotifications.StatRollbackEmailSenderJob)~limit~100~offset~0~reverseOrder~true~showTraceIdRelated~false))$)

### Какая функциональность пострадает от отказа джобы
Пользователи перестанут получать письма об откатах статистики.
В таблице ppc.stat_rollback_data начнут копиться данные.


### Как пользователи (или команда) заметят проблему и через какое время
Менеджеры заменят, что в рассыляторе не будет свежей статистики по отправкам писем.
Пользователи будут интересоваться у поддержки почему у них увеличилась сумма на счету.



### Контакты разработчиков и менеджеров

Разработчики: [Сергей Гукасьян](https://staff.yandex-team.ru/gukserg) <br/>
Менеджеры: [Михаил Иволгин](https://staff.yandex-team.ru/mivolgin)


### Желательное время исправления в случае поломки
Чинить в течение суток под присмотром app-duty



### Способы регулирования работы джобы
Джоба не регулируется.



### Известные причины поломок
Недоступность [Рассылятора](https://sender.yandex-team.ru/)



### Дополнительно: тонкости и подводные камни
Есть фича `new_stat_rollback_notification_enabled` для регулирования процента клиентов, которые будут получать новые письма от джобы.
В самой джобе эта фича не учитывается, она используется в скрипте [ppcStatRollbackNotify](https://a.yandex-team.ru/arc/trunk/arcadia/direct/perl/protected/ppcStatRollbackNotify.pl)
при добавлении записей в таблицу ppc.stat_rollback_data
