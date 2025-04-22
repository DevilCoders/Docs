## FeedUsageTypeProcessor

### Продукт/подсистема

Товарная реклама(Смарты, ДО, Фиды в ТГО).

### Роль в работе продукта/подсистемы

ESS-процессор, который отправляет в ```MBI``` информацию о том, как используются фиды в Директе, на основании этой информации
фиды прокачиваются в ```Datacamp``` или нет, выбирается пайплайн для офферов из этих фидов.
Если фид не использовался и стал использоваться, то тогда мы его включаем в MBI.

### Датафлоу

Обычный ESS процессор.

- Отслеживает события в таблице [feeds](https://direct-dev.yandex-team.ru/db/ppc/tables/feeds.html), а именно за полем ```usageTypes```.
- Отправляет информацию в ```MBI``` через http-ручку.


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.FeedUsageTypeProcessor.working.production&query=&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'usagetypes.FeedUsageTypeProcessor)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы

Не будут отправляться в ```MBI``` информация о типах использования фидов. А значит фиды могут не парситься или их оферы могут
не попадать в маркетный индекс или ```BannerLand```


### Как пользователи (или команда) заметят проблему и через какое время

Заметить непросто. Могут быть жалобы на неактуальные офферы в смартах или динамиках или отсутствие показов


### Контакты разработчиков и менеджеров

Разработчики: [buhter](https://staff.yandex-team.ru/buhter)
Менеджеры: [ulyashevda](https://staff.yandex-team.ru/ulyashevda)


### Желательное время исправления в случае поломки

ASAP, так как в итоге влияет на генерацию смартов и динамиков(факт генерации, скорость, актуальность)


### Способы регулирования работы джобы

- [Общие способы регулирования работы ESS-процессоров](../jobs-common.md#control-ess)


### Известные причины поломок

Отсутствуют.


### Дополнительно: тонкости и подводные камни

Отсутствуют.
