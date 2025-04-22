# direct.prod_mysql-health:ppcdata

[Алерт в juggler](https://juggler.yandex-team.ru/check_details/?host=direct.prod_mysql-health&service=ppcdata&query=&last=1DAY)


## Описание { #description }

Проверка показывает, что база ppcdata (все шарды) находится в нормальном рабочем состоянии.

Внутренние проверки (для каждой ppcdataN):

- db_availability_host_alive_ppcdataN &mdash; у шарда есть живой мастер
- db_availability_read_only_ppcdataN &mdash; красное означает, что мастер работает в readonly режиме
- db_availability_fresh_slave_ppcdataN &mdash; у шарда есть достаточно свежих реплик


## Диагностика { #diagnostics }

{% note alert "Быстро привлекай экспертов" %}

Перед тем, как начинать диагностику, позвони экспертам по БД:
- [yukaba@](https://staff.yandex-team.ru/yukaba/)
- [pe4kin@](https://staff.yandex-team.ru/pe4kin/)
- [dspushkin@](https://staff.yandex-team.ru/dspushkin/)

и скажи, что разбираешься с такой-то проверкой про базу

Поломки с базой разнообразны, инструкция и поиск по интернетам не научат, как быстро диагностировать и починить аварию.

{% endnote %}

Полезные инструменты:  
- схема репликации с отставаниями реплик: <https://observatorium.common.yandex.ru/storages/replication_schema>
- сделать запрос к шарду, с ppcback или ppcdev: `direct-sql pr:ppc:N 'select now()'` (`select 1` не используйте, он может работать когда ничего другое не работает)
- поискать в интерфейсе клиента из проблемного шарда
- на машине с базой `lm ppcdataN status`
- дашборды про mysql в мега-реестре <https://wiki.yandex-team.ru/direct/dash/infrastructure/>

## Решение { #solution }

Все по обстоятельствам, все вместе с экспертом.


## Ссылки { #links }

- Обсерваториум: <https://observatorium.common.yandex.ru/storages/replication_schema>
- Реестр графиков и алертов по инфраструктуре: <https://wiki.yandex-team.ru/direct/dash/infrastructure/>
- TODO: про lm
- релевантный код:
   - <https://a.yandex-team.ru/arc/trunk/arcadia/direct/infra/direct-utils/check-db-availability/bin/check-db-availability>
   - <https://a.yandex-team.ru/arc/trunk/arcadia/direct/infra/direct-utils/db-utils/opt/check-db-availability/check_db_utils.py>


## Воркфлоу { #workflow }

После переезда баз в MDB диагностика, методы решения и полезные ссылки поменяются.


