# coredump

## Настройки сбора и агрегации core-файлов (coredumps, корок) {#setup}

По умолчанию coredump-ы не собираются.

Чтобы включить их сборку для ворклоада с id `workloadId` из `DeployUnitId`, нужно добавить в спецификацию stage следующую минимальную конфигурацию:

```yaml
spec:
 deploy_units:
   DeployUnitId:
     coredump_config: 
       workloadId: 
         coredump_processor: 
           count_limit: 3
           probability: 100
           total_size_limit_megabytes: 1024
```

В этом случае stagectl добавит в под утилиту для сборки и агрегации coredumps [instancectl](https://sandbox.yandex-team.ru/resource/1536388832/view) и настроит её запуск через [porto](https://github.com/yandex/porto/blob/master/porto.md#coredumps).

### Смысл параметров {#parameters}

* `count_limit` — при превышении этого числа хранимых корок новые откладываться не будут.
* `total_size_limit_megabytes` — при превышении общего объёма диска, занятого корками, не откладывать следующую корку.
* `probability` — целое от 0 до 100. Вероятность в процентах, с которой очередная корка запишется в случае выполнения предыдущих условий.

### Имя и местонахождение {#name-path}

Coredump будет сохранён в боксе по следующему пути:

```
/coredumps_box/<stageId>_<workloadId>-<timestamp_ms>
```

где: `timestamp_ms` — unixtime момента сохранения.

В UI можно настроить сборку прямо на странице ворклоада.

## Агрегация {#aggregation}

Поддерживается получение трейсов из coredump'ов и их отправка в [агрегатор](https://wiki.yandex-team.ru/cores-aggregation). По умолчанию отправка трейсов в агрегатор выключена. Для включения отправки трейсов нужно в секции `coredump_processor` выставить параметр:

```yaml
 aggregator: 
   enabled: true
   url: aggregatorURL
   service_name: serviceName // имя сервиса (itype) для агрегатора. Опциональный, по умолчанию используется "deploy.<stageId>.<workloadId>"
   ctype: ctype // ctype для агрегатора, пустая строка по-умолчанию
```

{% note info %}

До 16.09.2020 `itype` в агрегаторе у всех coredump'ов был deploy, а строка `"<stageId>.<workloadId>"` проставлялась вместо хоста.

{% endnote %}

Для обработки coredump'ов используется [gdb](https://sandbox.yandex-team.ru/resource/1550153356/view), который будет принесён в бокс автоматически в случае включенной агрегации.

URL агрегатора можно не указывать, по-умолчанию используется [https://coredumps.yandex-team.ru/submit_core](https://coredumps.yandex-team.ru/submit_core)

Из проектной сети пода должен быть открыт HTTPS доступ в [панчере](https://puncher.yandex-team.ru) до `coredumps.yandex-team.ru` или альтернативной.

Настройки в UI на странице ворклоада.

## Удаление старых корок {#cleanup}

По умолчанию старые корки не удаляются, т.е. при превышении лимита на число или объём корок новые перестанут откладываться. Для того, чтобы включить чистку старых корок, необходимо в `coredump_processor` выставить целочисленный параметр `cleanup_ttl_seconds`, равный количеству секунд, после которого будут удалены старые корки. При этом старые корки будут удаляться только при попытке отложить новую корку. Если новых корок появляться не будет, то старые не будут удалены.

## Дополнительные ресурсы {#extra-resources}

Дополнительные ресурсы mem/cpu не требуются, так как обработка происходит после завершения работы ворклоада.
Требуется зарезервировать дополнительное место для утилит сбора и обработки корок — распакованных слоёв с instancectl и gdb (если включена агрегация).

## История изменений {#changelog}

Есть два вида ченджлога: один касается версии самого сайдкара, а другой — внешних его настроек (на базе runtime version).

### Изменения runtime version {#changelog-runtime}

* С [runtime version 7](../../../reference/patchers-revision.md#new-runtime-version-7) изменение логики приноса системных папок и вольюмов для writable папок в случае использования read only fs бокса.

