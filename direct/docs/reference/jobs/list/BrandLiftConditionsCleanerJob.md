## BrandLiftConditionsCleanerJob

### Продукт/подсистема

BrandLift - это фича для крупных клиентов, позволяющая оценить влияние охватной кампании на узнаваемость бренда с помощью специального опроса для части аудитории. Работает в интеграции с сервисом опросов Яндекс.Взгляд (aka "Пифия").


### Роль в работе продукта/подсистемы

Удаляет старые данные по оценкам охвата и бюджета кампаний с Brand Lift из таблицы [campaigns_budget_reach_daily](https://direct-dev.yandex-team.ru/db/ppc/tables/campaigns_budget_reach_daily.html). Сами старые данные на бизнес-логику не влияют, удаляем чтобы не засорять базу.


### Датафлоу

- [campaigns_budget_reach_daily](https://direct-dev.yandex-team.ru/db/ppc/tables/campaigns_budget_reach_daily.html)


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.BrandLiftConditionsCleanerJob.working.production&last=1DAY&query=)
- [Логи](https://direct.yandex.ru/logviewer#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'brandliftconditions.BrandLiftConditionsCleanerJob)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы

База будет засоряться устаревшими данными. Непосредственно на бизнес-логику не повлияет.


### Как пользователи (или команда) заметят проблему и через какое время

Никто не заметит.


### Контакты разработчиков и менеджеров

Разработчики: [Егор Иватько](https://staff.yandex-team.ru/ivatkoegor), [Катя Богуславская](https://staff.yandex-team.ru/eboguslavskaya) <br/>
Менеджеры: [Алексей Александров](https://staff.yandex-team.ru/hrustyashko), [Иван Мологин](https://staff.yandex-team.ru/chelu)


### Желательное время исправления в случае поломки

Неделя+.


### Способы регулирования работы джобы

Время жизни данных в базе находится в параметре `brand_lift/life_time_threshold` в конфиге [app-production.conf](https://a.yandex-team.ru/arc/trunk/arcadia/direct/jobs/src/main/resources/app-production.conf) приложения Jobs.


### Известные причины поломок




### Дополнительно: тонкости и подводные камни
