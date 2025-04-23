## BrandLiftConditionsDbQueueJob

### Продукт/подсистема

BrandLift - это фича для крупных клиентов, позволяющая оценить влияние охватной кампании на узнаваемость бренда с помощью специального опроса для части аудитории. Работает в интеграции с сервисом опросов Яндекс.Взгляд (aka "Пифия").


### Роль в работе продукта/подсистемы

Данный продукт предоставляется только крупным клиентам и бесплатно, поэтому важно запускать опросы только для "дорогих" кампаний. Джоба актуализирует оценки охвата и бюджета после изменения настроек кампании/группы. Это нужно для того, чтобы понять, достаточен ли охват и бюджет для запуска опроса.


### Датафлоу

- Из отдельного ess-процессора [BrandLiftRecalcProcessor](https://a.yandex-team.ru/arc/trunk/arcadia/direct/apps/event-sourcing-system/logicprocessor/src/main/java/ru/yandex/direct/logicprocessor/processors/brandliftrecalc/BrandLiftRecalcProcessor.java) id кампаний попадают в многофункциональную очередь [db_queue](https://direct-dev.yandex-team.ru/db/ppc/tables/dbqueue_jobs.html).
- Джоба берёт идентификаторы кампаний из [db_queue](https://direct-dev.yandex-team.ru/db/ppc/tables/dbqueue_jobs.html).
- Собирает оценки охвата из Inventori и бюджета для данных кампаний из [//home/yabs/stat/OrderStatDay](https://yt.yandex-team.ru/arnold/navigation?offsetMode=key&path=//home/yabs/stat/OrderStatDay).
- Пишет их в базу в [campaigns_budget_reach_daily](https://direct-dev.yandex-team.ru/db/ppc/tables/campaigns_budget_reach_daily.html).


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.BrandLiftConditionsDbQueueJob.working.production&query=&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'brandliftconditions.BrandLiftConditionsDbQueueJob)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)
- Мониторинг db_queue на возраст (которого на момент написания нет).


### Какая функциональность пострадает от отказа джобы

Пострадает автоматический запуск и остановка опросов после изменений в настройках кампании и её группах.
Не очень критично, так как есть еще дополнительная вторая джоба - [BrandLiftConditionsCollectorJob](BrandLiftConditionsCollectorJob.md), которая пересчитывает то же самое, но для всех кампаний, а не из очереди (она работает по ночам).


### Как пользователи (или команда) заметят проблему и через какое время

В настройках кампании не будет обновляться статус бренд-лифта.


### Контакты разработчиков и менеджеров

Разработчики: [Егор Иватько](https://staff.yandex-team.ru/ivatkoegor), [Катя Богуславская](https://staff.yandex-team.ru/eboguslavskaya) <br/>
Менеджеры: [Алексей Александров](https://staff.yandex-team.ru/hrustyashko), [Иван Мологин](https://staff.yandex-team.ru/chelu)


### Желательное время исправления в случае поломки

В течение суток.


### Способы регулирования работы джобы

В [app-production.conf](https://a.yandex-team.ru/arc/trunk/arcadia/direct/jobs/src/main/resources/app-production.conf) приложения Jobs в секции `brand_lift/db_queue` есть настройки для выборки заданий из DbQueue - размер пачки и время захвата задания.


### Известные причины поломок




### Дополнительно: тонкости и подводные камни

Есть возможность запускать и останавливать опросы вручную через ребят из Пифии.
