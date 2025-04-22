## ApproveCpmPriceCampaignFlightStatusApproveJob

### Продукт/подсистема

"Кампании с фиксированным CPM" ("прайсовая кампания") (`campaigns.type = 'cpm_price'`).


### Роль в работе продукта/подсистемы

В прайсовых кампаниях мы с клиентом заранее заключаем двустороннюю договоренность о периоде работы кампании и объеме трафика: с одной стороны мы бронируем для кампании часть трафика, а с другой - клиент обязуется этот трафик исчерпать.

Данная джоба для бронирований, которые ожидают подтверждение, делает запрос в Inventori о возможности бронирования траффика, и если это возможно - подтверждает бронь.


### Датафлоу

- Читаем из MySQL в поисках кампаний, которые ожидают подтверждения бронирования
- Делаем запросы в Inventori для найденных cid-ов
- Обновляем statusApprove=Yes в MySQL, если какие-либо кампании можно подтвердить


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.ApproveCpmPriceCampaignFlightStatusApproveJob.working.production&query=&last=1DAY)
- [Messages-лог](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'campaign.ApproveCpmPriceCampaignFlightStatusApproveJob)~limit~100~offset~0~reverseOrder~true~showTraceIdRelated~false))$)
- [Бинлоги](https://direct.yandex.ru/logviewer#~(logType~'binlog_rows_v2~form~(from~'20210524T000000~to~'20210524T235959~fields~(~'datetime~'source~'table~'service~'method~'primary_key~'operation~'row~'reqid)~conditions~(table~'campaigns_cpm_price~method~'campaign.ApproveCpmPriceCampaignFlightStatusApproveJob)~limit~100~offset~0~reverseOrder~true~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы

- Брони перестанут подтверждаться в автоматическом режиме, будет дополнительная нагрузка на ручное потверждение
- Клиенты будут дольше ожидать подтверждения бронирования


### Как пользователи (или команда) заметят проблему и через какое время?

Загорелся Juggler-мониторинг (сразу) или отсутствие апрува броней в бинлогах джобы длительное время (более 1-2 недель).


### Контакты разработчиков и менеджеров

Разработчики: [Олег Важнев](https://staff.yandex-team.ru/ovazhnev), [Андрей Павленко](https://staff.yandex-team.ru/andreypav) <br/>
Менеджеры: [Алексей Александров](https://staff.yandex-team.ru/hrustyashko)


### Желательное время исправления в случае поломки

В течении недели.


### Способы регулирования работы джобы

Настройки в секции `cpm_price_auto_approve` в [app-production.conf](https://a.yandex-team.ru/arc/trunk/arcadia/direct/jobs/src/main/resources/app-production.conf) приложения Jobs.


### Известные причины поломок

- Inventori недоступно


### Дополнительно: тонкости и подводные камни
