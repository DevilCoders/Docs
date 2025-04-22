# Logbroker (UnifiedAgent)

Отгрузкой логов занимается инфраструктурный sidecar-бокс `logbroker_tools_box`, в котором запущен Unified Agent.

## Ресурсы {#resources}

Для функционирования `logbroker_tools_box` на каждый под будут запрошены следующие ресурсы из вашей [квоты](../../../../reference/quotas-and-limits.md):

* 3 ГБ диска.
* 512 МБ RAM.
* 0.4 CPU.

Подробнее с запросом ресурсов на под можно ознакомиться [здесь](../../resource-requests.md).

### Пользовательское значение запрашиваемых ресурсов {#custom-resources}

Для некоторых ресурсов, запрашиваемых на `logbroker_tools_box`, доступна возможность настройки величины запроса.

Заказ ресурсов на бокс сайдкара состоит из двух частей:

- заказ на бокс (`for box`) — влияет на распределение ресурсов внутри пода;
- дополнительный заказ на весь под (`for pod`) — влияет на квоту.

{% note info %}

В случае использования дефолтных значений `for pod` равен `for box`, но в общем случае они могут различаться.

{% endnote %}

Пользовательские значения заказа ресурсов можно:

{% list tabs %}

- UI

  Настроить в разделе `Deploy unit settings (Form) / Logbroker config / Additional resources per pod` деплой-юнита.

  ![https://jing.yandex-team.ru/files/slamur/Screenshot%20from%202021-11-25%2015-04-47.png](https://jing.yandex-team.ru/files/slamur/Screenshot%20from%202021-11-25%2015-04-47.png)

- dctl

  Указать через поле деплой-юнита `logbroker_config.pod_additional_resources_request` типа [TResourceRequests](https://a.yandex-team.ru/arc/trunk/arcadia/yp/yp_proto/yp/client/api/proto/data_model.proto?rev=r8706994#L1363).

    Пример спеки:

    ```yaml
    spec:
    deploy_units:
        decreased_vcpu:
        logbroker_config:
            pod_additional_resources_request:
            vcpu_guarantee: 100
            vcpu_limit: 100
    ```

    Данное поле является опциональным, при отсутствии поля запрашиваются [дефолтные значения](../sidecars.md#quotas).

    {% note warning %}

    **Дефолтные значения** задаются только при отсутствии **всего поля** `logbroker_config.pod_additional_resources_request`.

    При отсутствии **отдельных полей внутри** указанного `pod_additional_resources_request` их значения будут считаться **равными 0**.

    {% endnote %}

    {% note warning %}

    Широкий тип `TResourceRequests` использован в целях возможности расширения набора изменяемых типов ресурсов в будущем.

    На данный момент только указанные поля реально используются для вычисления итоговой квоты:

      - `vcpu_guarantee`
      - `vcpu_limit`

    Значения остальных полей игнорируются при обработке.

    {% endnote %}


{% endlist %}


#### CPU {#custom-cpu}

Максимально разрешенное значение для `vcpu` — 32000 миллиядер.

{% note warning %}

Разрешены только **равные** значения `vcpu_limit` и `vcpu_guarantee`.

{% endnote %}

Итоговые значения ресурсов устанавливаются равными:

`for box`:
- `vcpu_guarantee` — пользовательскому значению;
- `vcpu_limit` — максимуму из дефолтного и пользовательского значений.

`for pod`:
- `vcpu_guarantee` — пользовательскому значению;
- `vcpu_limit` — пользовательскому значению.

{% note info %}

Ниже приведен пример вычисления заказываемых ресурсов.

Основной запрос на под равен (`main`):
- `vcpu_guarantee` = 0.8 cpu;
- `vcpu_limit` = 1.0 cpu.

Дефолтные значения для сайдкара логов равны (`default`):
- `vcpu_guarantee` = 0.4 cpu;
- `vcpu_limit` = 0.4 cpu.

Пользовательские значения запроса (`custom`):
- `vcpu_guarantee` = 0.3 cpu;
- `vcpu_limit` = 0.3 cpu.

Итоговые значения заказанных ресурсов на `logbroker_tools_box` (`for box`):
- `vcpu_guarantee` = `custom` = 0.3 cpu;
- `vcpu_limit` = max(`default`, `custom`) = 0.4 cpu.

Дополнительные значения заказанных ресурсов на весь под (`for pod`):
- `vcpu_guarantee` = `custom` = 0.3 cpu;
- `vcpu_limit` = `custom` = 0.3 cpu.

Итоговые значения заказанных ресурсов на весь под (`quota`):
- `vcpu_guarantee` = `main` + `for pod` = 1.1 cpu;
- `vcpu_limit` = `main` + `for pod` = 1.3 cpu.

{% endnote %}

## Ограничение потока данных {#limits}

Ограничение потока данных действует на Deploy Unit и задаётся двумя величинами:

- суммарный объём данных в секунду;
- количество сообщений в секунду.

{% note info %}

Ограничения применяются к <b>оригинальному объёму</b> передаваемых данных.

Сжатие данных, производимое Unified Agent, применяется уже после отсечения данных по ограничениям.

{% endnote %}

### Абсолютное ограничение
При использовании стандартного механизма отгрузки логов (независимо, автоматическая отгрузка или через библиотеки), существует <b>абсолютное ограничение</b>:

- 1 терабайт в секунду;
- 100500 сообщений в секунду.

### Ограничения для коммунального топика

Так как коммунальный топик сохраняет данные всех пользователей в одну таблицу, то для него действуют усиленные ограничения:

- при использовании [Runtime version 7](../../../../reference/patchers-revision.md#runtime-version-7) или выше:

    - 15 мегабайт в секунду
    - 20000 сообщений в секунду

### Ограничение срока хранения данных в YDB

Срок хранения данных в YDB составляет `2 суток`, после чего таблицы с данными удаляются.


## Дополнительная настройка сайдкара логов

### Развертывание сайдкара логов без использования автоматической отгрузки stdout/stderr {#mandatory-logbroker-box}

Предусмотрено развертывание сайдкара логов без активации [автоматической отгрузки `stdout`/`stderr`](#auto-stdout-stderr).

Это является актуальным, если пользователь организует отгрузку только через [клиентские библиотеки](#libs).

Функционал активируется выставлением значения `mandatory` для поля `sidecar_bringup_mode`([proto конфигурация](https://arcanum.yandex-team.ru/arc/trunk/arcadia/yp/yp_proto/yp/client/api/proto/stage.proto?rev=r8809600#L526)):

```yaml
spec:
  deploy_units:
    deploy_unit:
      logbroker_config:
        sidecar_bringup_mode: mandatory
```

### Пользовательские настройки destroy policy

Аналогично основному приложению, у сайдкаров есть сценарии различных этапов жизненного цикла, в том числе [удаления из пода](../../workload/probes.md#destroy-policy).

В данный момент существуют следующие настройки и ограничения для данного сценария:

**Значение** | **Описание** | **Значение по умолчанию** | **Ограничения** |
:--- | :--- | :--- | :---
`max_tries` | максимальное количество попыток запуска сценария | 3 | Неотрицательное число
`restart_period_ms` | интервал времени между попытками в миллисекундах | 10000 мс | Не менее 10000 мс
`(max_tries - 1) * restart_period_ms` | суммарное время ожидания между попытками | | Не более 5 часов

Конфигурация сценария задана следующим [proto message](https://a.yandex-team.ru/arc/trunk/arcadia/yp/yp_proto/yp/client/api/proto/stage.proto?rev=r8445836#L528).

Пример спеки деплой юнита с указанными настройками:

```yaml
spec:
    deploy_units:
        deploy_unit_id:
            logbroker_config:
                destroy_policy:
                    max_tries: 5
                    restart_period_ms: 20000
```

{% note tip %}

Оба поля являются опциональными, можно указать только необходимую для изменения настройку.

{% endnote %}


## История изменений {#changelog}

Есть два вида ченджлога: один касается версии самого сайдкара, а другой — внешних его настроек (на базе runtime version).

* Доступна настройка CPU бокса (влияет на общую квоту на под). Итоговое поведение описано в [документации](../logs/logs.md#custom-resources). На UI добавлено зануление CPU в разделе **Logbroker config. Additional resources per pod**.

