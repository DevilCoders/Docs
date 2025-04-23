### Продукт/подсистема

Товарная реклама (смарты, ДО).

### Роль в работе продукта/подсистемы

Синхронизирует используемость фидов с заданиями на генерацию в BannerLand.
Используемыми считаются те фиды, что прокачаны в MBI/DataCamp (т.е. для них есть `BusinessID` и `ShopID`)
и по которым есть с соответствующими ID активные задания на генерацию в BLRT.
Все остальные фиды считаем неиспользуемыми. Используемые фиды затем включаются в MBI (`FeedUsageTypeProcessor`),
а неиспользуемые через некоторое время выключаются (`DisableFeedsInMBIJob`), чтобы не создавать лишней нагрузки.

При этом используемость фидов пересчитывается еще и в `RecalculateFeedUsageTypeProcessor`,
который в целом обеспечивает работу системы, но иногда отстает или теряет что-то, пропуская события или не учитывая какие-то кейсы.
Эта джоба же с задержкой в несколько минут обеспечивает 100% точность используемости фидов.

### Датафлоу

Достает из динамических таблиц BLRT ([task/dyn/FeedToTasks](https://yt.yandex-team.ru/hahn/navigation?offsetMode=key&path=//home/blrt/task/dyn/FeedToTasks)
и [task/perf/FeedToTasks](https://yt.yandex-team.ru/hahn/navigation?offsetMode=key&path=//home/blrt/task/perf/FeedToTasks))
все пары (`BusinessID`, `ShopID`), по которым есть задания на генерацию.

Достает из MySQL все фиды, пролитые в MBI/DataCamp.

Всем полученным из MySQL фидам обновляет используемость, проверяя, есть ли они среди выгруженных из динамических таблиц BLRT.

### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&last=1DAY&service=jobs.RecalculateFeedsUsageTypesJob.working.production)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'feed.RecalculateFeedsUsageTypesJob)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)

### Какая функциональность пострадает от отказа джобы

Пересчет используемости фидов ляжет полностью на плечи `RecalculateFeedUsageTypeProcessor`.
В силу его описанной выше несовершенности, информация об их используемости некоторых фидов может стать некорректной, 
из-за чего эти фиды могут быть вовремя не включены/выключены в MBI.

### Как пользователи (или команда) заметят проблему и через какое время

В случае отказа джобы, из-за того, что какие-то фиды могут не быть вовремя включены в MBI,
пользователи в редких случаях могут столкнуться с отсутствием показов или неактуальными офферами в смартах или ДО.
Длительное нарушение работоспособности, из-за которого неиспользуемые фиды могут не быть выключены в MBI,
также может повлечь возрастание объема данных в DataCamp и общей нагрузки на инфраструктуру Маркета.

### Контакты разработчиков и менеджеров

Разработчики: [ali-al](https://staff.yandex-team.ru/ali-al) 
<br/>
Менеджеры: [ulyashevda](https://staff.yandex-team.ru/ulyashevda)

### Желательное время исправления в случае поломки

День
