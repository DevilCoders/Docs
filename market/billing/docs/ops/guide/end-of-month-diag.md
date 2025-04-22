# Конец месяца: как понять, что все успешно


## За чем следить

### Синий Биллинг и маркетинговые услуги

Скрипты:
* <https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/infra/diagnostics/end-of-month/bill-results-completeness.sh> -- даты, на которых остановились биллинги. В норме -- вчерашняя дата. Фильтрацию "что работает еще в Oracle, что еще в PG" делаем в уме
* <https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/infra/diagnostics/end-of-month/tlog-collected.sh> -- все ли результаты обилливаний собрали в tlog
* <https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/infra/diagnostics/end-of-month/tlog-exported.sh> -- весь ли tlog экспортировали в YT

### Международный биллинг

Скрипты:
* Для проверки, что даты обилливания совпадают с текущей запустит скрипт [bill-global-completeness.sh](https://a.yandex-team.ru/arcadia/market/billing/infra/diagnostics/end-of-month/bill-global-completeness.sh)
* Для услуг запустит скрипт [tlog-global-collected.sh](https://a.yandex-team.ru/arcadia/market/billing/infra/diagnostics/end-of-month/tlog-global-collected.sh)
* Для УВ запустить скрипт [global-payment-control.sh](https://a.yandex-team.ru/arcadia/market/billing/infra/diagnostics/end-of-month/global-payment-control.sh)

### Управление выплатами

Скрипты:
* <https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/infra/diagnostics/end-of-month/payment-control.sh> — проверяем, что:
  * все начисления (`accrual`) выгрузились в соответствующий tlog;
  * все команды на выплату (`payment-order`) выгрузились в соответствующий tlog;
  * все записи из обоих tlog'ов (`payments_payouts_transaction_log` и `expenses_payouts_transaction_log`) выгрузились в YT.

### Логистика

Скрипты:
* <https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/infra/diagnostics/end-of-month/logistics.sh> -- смотрим, что за прошлый месяц есть записи и их достаточно много


### Другое?

* Дистрибуция?


## Ссылки

* <https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/infra/diagnostics/end-of-month> -- набор проверочных скриптов к закрытию месяца
* <https://a.yandex-team.ru/arc_vcs/market/billing/infra/mb-sql/README.md> -- инструкция по настройке консольного скрипта для похода в БД

