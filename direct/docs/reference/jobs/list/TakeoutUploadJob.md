## TakeoutUploadJob
### Продукт/подсистема
Выгрузка данных по запросу пользователя в соответствии с генеральным регламентом о защите данных (General Data Protection Regulation, сокращенно GDPR)



### Роль в работе продукта/подсистемы
Выгрузка данных о клиенте Директа в ручку Паспорта по GDPR-запросу



### Датафлоу
- Берет задания из очереди [DBQueue](https://direct-dev.yandex-team.ru/db/ppc/tables/dbqueue_jobs.html)
- Полчает данные о клиенте директа из базы
- Если данные нашлись, то загружает их в Паспортную ручку [upload](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs/takeout-client/src/main/java/ru/yandex/direct/takeout/client/TakeoutClient.java?#L55)
- Вызывает Паспортную ручку [upload/done](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs/takeout-client/src/main/java/ru/yandex/direct/takeout/client/TakeoutClient.java?#L61)
- Отмечает задание в очереди выполненным


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.TakeoutUploadJob.working.production&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'takeout.TakeoutUploadJob)~limit~100~offset~0~reverseOrder~true~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы
Паспорт не сможет получить данные о клиенте Директа для выгрузки данных в соответствии с GDPR



### Как пользователи (или команда) заметят проблему и через какое время
Пользователи не смогут получить выгрузку своих данных.<br/>
К команде Директа придут дежурные Паспорта.


### Контакты разработчиков и менеджеров

Разработчики: [Роман Кухта](https://staff.yandex-team.ru/kuhtich) <br/>


### Желательное время исправления в случае поломки
Чинить в течение суток под присмотром app-duty



### Способы регулирования работы джобы
Джоба не регулируется



### Известные причины поломок




### Дополнительно: тонкости и подводные камни
Заданий на выгрузку данных очень мало, большую часть времени джоба простаивает.
