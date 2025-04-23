## UacUpdateStatusesProcessor

### Продукт/подсистема

UAC

### Роль в работе продукта/подсистемы
Синхронизирует статус модерации, флаги, причины отклонения баннеров с контентами и заявками в Ydb Uac.

### Датафлоу

- Следит за изменениями статусов баннера, флагами баннера, изменениями причин отклонения
- Для измененных объектов пересчитывает статусы, флаги, причины отклонения контента

При изменении баннера пересчитываются все данные по кампании, так как контенты присутствуют в нескольких баннерах кампании

### Способы наблюдения за текущим состоянием
- [Отставание по шардам](https://solomon.yandex-team.ru/?project=direct&cluster=app_java-jobs&service=java-monitoring&l.host=CLUSTER&l.sensor=binlog_delay&l.shard=*&graph=auto&l.ess_processor=uac_update_statuses&stack=false&b=1d&e=)
- [Количество обработанных объектов по шардам](https://solomon.yandex-team.ru/?project=direct&cluster=app_java-jobs&service=java-monitoring&l.host=CLUSTER&l.sensor=logic_objects_count&l.shard=*&graph=auto&l.ess_processor=uac_update_statuses&transform=differentiate&b=1d&e=)
- [График отставания вычитки топика ESS-роутером](https://solomon.yandex-team.ru/?project=kikimr&cluster=lbkx&service=pqtabletAggregatedCounters&l.ConsumerPath=direct%2Fess%2Fess-consumer&l.OriginDC=Kafka-bs&l.sensor=CreateTimeLagMsByCommitted&l.host=dc-unknown&graph=auto&l.TopicPath=direct%2Fess%2Fuac-update-statuses&b=1d&e=)

### Какая функциональность пострадает от отказа джобы
Синхронизация статусов кампании и контента из mysql в YDB

### Как пользователи (или команда) заметят проблему и через какое время
Пользователи могут заметить, что контенты не показываются, хотя статус активен

### Контакты разработчиков и менеджеров

Разработчики: [Марина Спиридонова](https://staff.yandex-team.ru/mspirit), [Сергей Димитров](https://staff.yandex-team.ru/dimitrovsd)

### Желательное время исправления в случае поломки

Как можно раньше.

### Способы регулирования работы джобы

- [Общие способы регулирования работы ESS-процессоров](../jobs-common.md#control-ess)

### Известные причины поломок

- Проблемы с LogBroker, ESS, YDB
