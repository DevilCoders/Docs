# Наблюдаемость: Синий Биллинг

**Для кого:** разработка

Ссылка | Про что это
:--- | :---
<https://grafana.yandex-team.ru/d/DEEmxlxik/mbi-events-log?orgId=1> | Oracle-GOE
<https://solomon.yandex-team.ru/?project=market-billing&cluster=agent-metrics&service=market-billing-tms&l.sensor=not_exported_to_tlog_transactions.count.*&graph=auto&l.host=*&b=1d&e=> | Новый полосатый график сбора в tlog
<https://monitoring.yandex-team.ru/projects/market-billing/dashboards/mon3snnhroupqt6ro2ut/view> | Еще один график про сбор в tlog (но не экспорт!)
<https://juggler.yandex-team.ru/check_details/?host=market-billing&service=logbroker_pg_reading&project=market-billing> | Отставания PG-GOE
<https://juggler.yandex-team.ru/check_details/?host=market-billing&service=logbroker_pg_reading&project=market-billing> | Игнорируемые события в PG-GOE
<https://grafana.yandex-team.ru/d/se9flA8Mk/report-generator?orgId=1&from=now-3h&to=now&refresh=5s> | Дашборд про отчеты (report-generator)

Про биллинги, сбор и экспорт tlog в YT также см. проверочные скрипты к концу месяца:
* <https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/infra/diagnostics/end-of-month>
* [{#T}](../../ops/guide/end-of-month-diag.md)

