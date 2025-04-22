## CampaignStatusCorrectCheckProcessor

### Продукт/подсистема

Кампания с фиксированным CPM (прайсовые кампании, `ppc.campaigns.type = 'cpm_price'`) для Главной Страницы.


### Роль в работе продукта/подсистемы

В прайсовых кампаниях для Главной Страницы мы с клиентом заранее заключаем двустороннюю договоренность о периоде работы кампании и объеме трафика: с одной стороны мы бронируем для кампании часть трафика, а с другой - клиент обязуется этот трафик исчерпать (для этого он должен к моменту старта кампании создать в ней баннеры требуемых форматов и пройти модерацию). Пригодность кампании к открутке отражается в статусе `status_correct` в таблице [campaigns_cpm_price](https://direct-dev.yandex-team.ru/db/ppc/tables/campaigns_cpm_price.html). От этого статуса зависит, будет ли кампания крутиться. Данная джоба реагирует на изменения в объектах кампании и пересчитывает этот статус.

### Датафлоу

ESS-процессор.
- Реагирует на изменения в объектах внутри кампании (группы, баннеры...).
- Пересчитывает статус.
- Выставляет статус `status_correct` в таблице [campaigns_cpm_price](https://direct-dev.yandex-team.ru/db/ppc/tables/campaigns_cpm_price.html).


### Способы наблюдения за текущим состоянием

- [Общий дашборд ESS](https://solomon.yandex-team.ru/?project=direct&dashboard=ess&project=direct&cluster=app_binlogbroker&service=java-monitoring&env=production&b=2021-03-14T09%3A41%3A19.102Z&e=2021-03-15T09%3A41%3A19.102Z)
- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.CampaignStatusCorrectCheckProcessor.working.production&query=&last=1DAY) - так же загорится, если отставание обработки событий превышает 5 минут.
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'campaignstatuscorrect.CampaignStatusCorrectCheckProcessor)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы

Критично: прайсовые кампании для главной страницы не смогут уйти в показы, а это как правило крупные клиенты и большие деньги.


### Как пользователи (или команда) заметят проблему и через какое время

Пользователи будут видеть в интерфейсе, что кампания находится в статусе "некорректно".


### Контакты разработчиков и менеджеров

Разработчики: [Арнольд Таммемяги](https://staff.yandex-team.ru/aleran), [Олег Важнев](https://staff.yandex-team.ru/ovazhnev), [Сергей Белоусов](https://staff.yandex-team.ru/mexicano)


### Желательное время исправления в случае поломки

Как можно скорее.


### Способы регулирования работы джобы

- [Общие способы регулирования работы ESS-процессоров](../jobs-common.md#control-ess)


### Известные причины поломок




### Дополнительно: тонкости и подводные камни
