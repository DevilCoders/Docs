# direct.prod_mysql-health:ppcdict

[juggler](https://juggler.yandex-team.ru/check_details/?service=ppcdict&host=direct.prod_mysql-health&last=1DAY)


## Описание { #description }

Проверка показывает, что база ppcdict находится в нормальном рабочем состоянии.

Внутренние проверки:

- db_availability_host_alive_ppcdict &mdash; есть живой мастер
- db_availability_read_only_ppcdict &mdash; красное означает, что мастер работает в readonly режиме
- db_availability_fresh_slave_ppcdict &mdash; есть достаточно свежих реплик
- db_availability_semisync_master_ppcdict — текущий мастер работает в режиме semisync репликации (есть с чего реплицировать)
- db_availability_semisync_slaves_ppcdict — на слевайх semisync режим репликации (если его отключить, а на мастере оставить — транзакции зависнут в ожидании)

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
- сделать запрос к шарду, с ppcback или ppcdev: `direct-sql pr:ppcdict 'select now()'` (`select 1` не используйте, он может работать когда ничего другое не работает)
- на машине с базой `lm ppcdict status`
- дашборды про mysql в мега-реестре <https://wiki.yandex-team.ru/direct/dash/infrastructure>

## Решение { #solution }

Все по обстоятельствам, все вместе с экспертом.


## Ссылки { #links }

- Обсерваториум: <https://observatorium.common.yandex.ru/storages/replication_schema>
- Реестр графиков и алертов по инфраструктуре: <https://wiki.yandex-team.ru/direct/dash/infrastructure>
- TODO: про lm
- релевантный код:
   - <https://a.yandex-team.ru/arc/trunk/arcadia/direct/infra/direct-utils/check-db-availability/bin/check-db-availability>
   - <https://a.yandex-team.ru/arc/trunk/arcadia/direct/infra/direct-utils/db-utils/opt/check-db-availability/check_db_utils.py>


## Воркфлоу { #workflow }

После переезда баз в MDB диагностика, методы решения и полезные ссылки поменяются.


