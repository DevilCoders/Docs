## RecalculateFeedUsageTypeProcessor

### Продукт/подсистема

Товарная реклама(Смарты, ДО, Фиды в ТГО).

### Роль в работе продукта/подсистемы

ESS-процессор, который пересчитывает информацию об использовании фидов в Директе. Тем, которые нигде не использовались,
но стали использоваться, проставляет соответственный usage_types. Если фид перестал использоваться, то сбрасывает
usage_types и проставляет last_used в now() (чтобы спустя время джоба DisableFeedsInMBIJob выключила их в MBI)
Делает это на основании привязки фидов к группам разных типов, а так же агрегированных статусов групп и кампаний, к
которым привязаны фиды. Если фид нигде не использовался, но теперь стал — то включаем фид в MBI по market_shop_id

### Датафлоу

Обычный ESS процессор.

- Отслеживает события в таблицах
    - [adgroups_dynamic](https://direct-dev.yandex-team.ru/db/ppc/tables/adgroups_dynamic.html) — для ДО
    - [adgroups_performance](https://direct-dev.yandex-team.ru/db/ppc/tables/adgroups_performance.html) — для Смартов
    - [adgroups_text](https://direct-dev.yandex-team.ru/db/ppc/tables/adgroups_text.html) — для ТГО(Смарт+ДО+ТГО)
    - [aggr_statuses_adgroups](https://direct-dev.yandex-team.ru/db/ppc/tables/aggr_statuses_adgroups.html) — для
      статусов групп(все типы)
    - [aggr_statuses_campaigns](https://direct-dev.yandex-team.ru/db/ppc/tables/aggr_statuses_campaigns.html) — для
      статусов кампаний(все типы)
- Обновляет ```usage_types``` в таблице [feeds](https://direct-dev.yandex-team.ru/db/ppc/tables/feeds.html) в
  соответствии с полученными данными, что в свою очередь инициирует ```FeedUsageTypeProcessor```

### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.RecalculateFeedUsageTypeProcessor.working.production&query=&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'usagetypes.RecalculateFeedUsageTypeProcessor)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)

### Какая функциональность пострадает от отказа процессора

Не будет обновляться информация об использовании фидов, а значит она не будет отправляться в ```MBI```. А значит фиды
могут не парситься или их офферы могут не попадать в маркетный индекс или ```BannerLand```
Выключенные ранее в MBI фиды не будут включаться

### Как пользователи (или команда) заметят проблему и через какое время

Заметить непросто. Могут быть жалобы на неактуальные офферы в смартах или динамиках или отсутствие показов

### Контакты разработчиков и менеджеров

Разработчики: [buhter](https://staff.yandex-team.ru/buhter)
Разработчики: [kozobrodov](https://staff.yandex-team.ru/kozobrodov)

Менеджеры: [ulyashevda](https://staff.yandex-team.ru/ulyashevda)

### Желательное время исправления в случае поломки

ASAP, так как в итоге влияет на генерацию смартов и динамиков(факт генерации, скорость, актуальность)

### Способы регулирования работы джобы

- [Общие способы регулирования работы ESS-процессоров](../jobs-common.md#control-ess)

### Известные причины поломок

Отсутствуют.

### Дополнительно: тонкости и подводные камни

Отсутствуют.
