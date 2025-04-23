## BrandLiftConditionsCollectorJob

### Продукт/подсистема

BrandLift - это фича для крупных клиентов, позволяющая оценить влияние охватной кампании на узнаваемость бренда с помощью специального опроса для части аудитории. Работает в интеграции с сервисом опросов Яндекс.Взгляд (aka "Пифия").


### Роль в работе продукта/подсистемы

Данный продукт предоставляется только крупным клиентам и бесплатно, поэтому важно запускать опросы только для "дорогих" кампаний. Джоба актуализирует оценки охвата и бюджета, чтобы понять, достаточен ли охват и бюджет для запуска опроса.


### Датафлоу

- Джоба собирает из YT все кампании с BrandLift-ом и там же джойнит статистику по деньгам - так получается список кампаний с оценкой бюджета.
- С этим списком идёт в инвентори за охватом.
- Складывает оценку охвата в базу в [campaigns_budget_reach_daily](https://direct-dev.yandex-team.ru/db/ppc/tables/campaigns_budget_reach_daily.html).


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.BrandLiftConditionsCollectorJob.working.production&last=1DAY&query=)
- [Логи](https://direct.yandex.ru/logviewer#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'*25BrandLiftConditionsCollectorJob)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы

Пострадает автоматический запуск и остановка опросов. Данная функциональность частично дублируется джобой [BrandLiftConditionsDbQueueJob](BrandLiftConditionsDbQueueJob.md), поэтому отказ не является чем-то супер критичным. В любом случае надо уведомить кого-нибудь из контактов.


### Как пользователи (или команда) заметят проблему и через какое время

Пользователи увидят, что их опрос не стартовал в течение суток.


### Контакты разработчиков и менеджеров


Разработчики: [Егор Иватько](https://staff.yandex-team.ru/ivatkoegor), [Катя Богуславская](https://staff.yandex-team.ru/eboguslavskaya), [Саид Аммаев](https://staff.yandex-team.ru/ammsaid) <br/>
Менеджеры: [Алексей Александров](https://staff.yandex-team.ru/hrustyashko), [Иван Мологин](https://staff.yandex-team.ru/chelu)


### Желательное время исправления в случае поломки

Дни.


### Способы регулирования работы джобы

В большинстве случаев до недели.


### Известные причины поломок

Самая крупная поломка была из-за кривого креатива в базе, который кидал исключение при сборе данных для запроса в Инвентори.


### Дополнительно: тонкости и подводные камни
