# downtime-db.*
Через точку указывается имя базы, например:
- downtime-db.ppcdata1
- downtime-db.ppcdict
- downtime-db.ppcmonitor
- downtime-db.sandbox

[Все проверки в juggler](https://juggler.yandex-team.ru/aggregate_checks/?query=service%3Ddowntime-db.*&limit=40).

## Описание { #description }
Мастер базы данных попадает под запланированныое отключение ДЦ (учения/работы). 

## Диагностика { #diagnostics }
Данные о запланированных отключениях кешируем в ZK:
```sh
direct-zkcli ls /direct/hosts-downtimes
```

В описании события в Juggler есть id события в infra.
Посмотреть на событие можно по ссылке вида `https://infra.yandex-team.ru/event/<id события>`.

Может оказаться, что работы/учения отменили или перенесли на другой день. 

{% note info "Если хост на самом деле в другом ДЦ" %}

Если отключаемый кластер не совпадает с кластером хоста, на котором загорелась проверка, проверить, что в [alldb-config](https://a.yandex-team.ru/arc/trunk/arcadia/direct/infra/direct-utils/zk-sync/confs/alldb-config.json) для хоста указан верный кластер.

{% endnote %}

## Решение { #solution }

Если отключение ДЦ актуально: переключить мастеров из отключаемого ДЦ.

Если отключение ДЦ отменили или перенесли: вручную удалить запись из ZK (автоматика только добавляет записи и ничего не удаляет). 

