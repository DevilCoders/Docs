## BrandLiftRecalcProcessor

### Продукт/подсистема

BrandLift - это фича для крупных клиентов, позволяющая оценить влияние охватной кампании на узнаваемость бренда с помощью специального опроса для части аудитории. Работает в интеграции с сервисом опросов Яндекс.Взгляд (aka "Пифия").


### Роль в работе продукта/подсистемы

Помогает оперативно пересчитать статус брендлифта на кампанию после изменения кампании пользователем. Складывает в DBQueue очередь кампании с брендлифтом для пересчета. Активизируется через ESS при изменении данных в кампании, группе, баннере, корректировках в БД. В дальнейшем пересчет ведется в [BrandLiftConditionsDbQueueJob](BrandLiftConditionsDbQueueJob.md).


### Датафлоу

ESS-процессор.

- Следит за изменениями в ess-rule [BrandLiftRecalcRule](https://a.yandex-team.ru/arc_vcs/direct/apps/event-sourcing-system/router/src/main/java/ru/yandex/direct/ess/router/rules/brandliftrecalc/BrandLiftRecalcRule.java).
- Для проверки наличия брендлифта берет данные из [ppc.camp_options](https://direct-dev.yandex-team.ru/db/ppc/tables/camp_options.html) (`camp_options.brand_survey_id != null`).
- Добавляет задания на пересчет статуса бренд-лифта [ppc.dbqueue_jobs](https://direct-dev.yandex-team.ru/db/ppc/tables/dbqueue_jobs.html).


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.BrandLiftRecalcProcessor.working.production&query=&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'brandliftrecalc.BrandLiftRecalcProcessor)~limit~100~offset~0~reverseOrder~true~showTraceIdRelated~false))$)


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




### Известные причины поломок




### Дополнительно: тонкости и подводные камни

