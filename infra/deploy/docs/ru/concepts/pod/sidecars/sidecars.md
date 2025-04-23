# Sidecar

**Sidecar** (сайдкар) — это паттерн проектирования облачных систем. Заключается в том, что часть функциональности приложения (например, отправка логов, service discovery) выносится в отдельный контейнер, который поднимается рядом с основным приложением и взаимодействует с ним по локальному интерфейсу. В Y.Deploy таким образом реализуется интеграция с частями инфраструктуры.

{% note info %}

Подробнее о паттернах `composite containers`: [https://kubernetes.io/blog/2015/06/the-distributed-system-toolkit-patterns/](https://kubernetes.io/blog/2015/06/the-distributed-system-toolkit-patterns/).

{% endnote %}

Каждый sidecar требует вычислительных ресурсов на запуск, которые будут запрошены из ABC-квоты **в дополнение к тем ресурсам, которые указал пользователь** (т.е. если пользователь попросил на под 2 ядра и и добавил еще 1 сайдкар, который требует 0,3 ядра, то на под будет аллоцированно 2,3 ядра).

Запрос ресурсов и создание sidecar происходят только в том случае, если пользователь включил в своем deploy unit соответствующую функциональность. Указывается отдельно для каждого deploy unit.

## Общая информация о доступных сайдкарах {#table}

Название Sidecar | Для чего используется | Мультипликатор | В каких случаях добавляется
:--- | :--- | :--- | :---
PodAgent | Инфраструктурный sidecar, который выступает в роли гипервизора | Pod | Всегда
[Logbroker(UnifiedAgent)](logs/logs.md) | Поставка логов | Pod | Если пользователь включил поставку логов для подов данного Deploy Unit
[Juggler subagent](jugglersubagent.md)  | Для запуска Juggler-проверок в пользовательском Box | Box | Если пользователю требуется запустить Juggler subagent в в данном Box
[TVM tool](tvmtool.md)                 | Для работы с TVM | Pod | Если требуется обеспечить взаимодействие между сервисами с использованием механизмов TVM
[Coredump](coredump.md)                 | Если у пользователя есть необходимость собирать coredumps для последующего анализа | WorkLoad | Если пользователь включил агрегацию coredumps
[Logrotate](logrotate.md)               | Для ротации логов в пользовательском Box | Box | Если пользователь включил ротирование логов

## Квота для сайдкаров {#quotas}

Дополнительные запросы квоты для сайдкаров указаны в следующей таблице. `custom` — значения, которые можно переопределять в спецификации стейджа. В скобках указаны дефолтные значения.

Нули означают, что ресурсы, потребляемые сайдкаром, будут взяты из основной квоты пода в спеке стейджа.

Если версии рантайма нет, то значения наследуют из ближайшей предыдущей ревизии.

Сайдкар                                        | [Версия рантайма](../../../reference/patchers-revision.md) | CPU | Mem | Disk
:---                                           | :--- | :--- | :--- | :---
PodAgent                                       | ≥ 1 | 0 | 0 | 1 GB
[Juggler subagent](#juggler-subagent)          | ≥ 1 | 0.13 CPU | 256 MB | 0
_                                              | [≥ 2](../../../reference/patchers-revision.md#runtime-version-2) | 0.13 CPU | 256 MB | 512 MB
[TVM tool](#tvm-tool)                          | ≥ 1 | max(`custom`, 0.1 CPU) | max(`custom`, 30 MB) | 950 MB
_                                              | [≥ 3](../../../reference/patchers-revision.md#runtime-version-3) | `custom` (0.1 CPU)  | `custom` (30 MB) | 950 MB
[Dynamic Resource](#dynamic-resource)          | ≥ 1 | 0 | 0 | 0
_                                              | [≥ 3](../../../reference/patchers-revision.md#runtime-version-3) | 0.1 CPU | 128 MB | 0
[Logbroker (UnifiedAgent)](#logbroker)         | ≥ 1 | `custom` (0.4 CPU) | 512 MB | 3 GB
Coredump                                       | ≥ 1 | 0 | 0 | 0
Logrotate                                      | ≥ 1 | 0 | 0 | 0

### Детали {#details}

#### Juggler subagent {#juggler-subagent}

* В [runtime version 2](../../../reference/patchers-revision.md#fix-runtime-version-2) исправлено выставление дисковой квоты на juggler workload. Теперь выставляется [512MB HDD на каждый box](../concepts/pod/sidecars/sidecars#quotas).

Подробнее об изменениях см. [{#T}](jugglersubagent.md).

#### TVM Tool {#tvm-tool}

* До [runtime version 3](../../../reference/patchers-revision.md#new-runtime-version-3) брались максимальные значения из дефолтных и указанных пользователем.

Подробнее об изменениях см. [{#T}](tvmtool.md).

#### Dynamic Resource {#dynamic-resource}

* До [runtime version 3](../../../reference/patchers-revision.md#new-runtime-version-3) ресурсы брались из общей квоты пода.

Подробнее об изменениях см. [{#T}](../../dynamic-resources.md).

#### Logbroker (UnifiedAgent) {#logbroker}

* Доступна настройка CPU бокса (влияет на общую квоту на под).

Подробнее об изменениях см. [{#T}](logs/logs.md).

### Ожидаемые изменения {#changes}

**PodAgent**: будет запрашивать дополнительно CPU и Memory ([DEPLOY-4532](https://st.yandex-team.ru/DEPLOY-4532)).

## Обновление сайдкаров {#updates}

Если деплой-юнит содержит версию сайдкара ниже последней рекомендуемой, во время редактирования через UI будет предложено обновить [спецификацию stage](https://a.yandex-team.ru/arc/trunk/arcadia/yp/yp_proto/yp/client/api/proto/stage.proto?rev=r8380085#L212-216) новым значением версии.

{% note warning %}

Настоятельно не рекомендуется оставлять поля с версиями сайдкаров пустыми — это может привести к автоматическому обновлению версии сайдкара вместе с вашим релизом без предупреждения.

{% endnote %}

Рекомендуется соглашаться на обновление в UI между вашими релизами (прокатить специально обновления сайдкаров без ваших изменений).
Это позволит разделить релизы сайдкаров и ваши релизы, понизив риск возможных неприятных последствий от обновления сайдкара во время важного релиза.

Существует возможность автоматически обновлять сайдкары и рантайм версии. Когда происходит релиз сайдкаров и [Runtime version](../../../reference/patchers-revision.md), мы помечаем стейдж как доступный для обновления. С любой последующей выкладкой stage доступное обновление применится, обновление отобразится будет видно в diff после выкладки.

{% note info %}

Для production сервисов, мы рекомендуем разделять релизы инфраструктуры и сервиса.

{% endnote %}

Обновления предлагаются через UI и их нужно применять, а для пользователей автоматических выкладок можно использовать утилиту [dctl](../../../reference/tools/dctl.md):

```bash
ya dctl sidecar update amich-stage -c xdc
```

{% list tabs %}

- UI

  Включить в настройках Deploy Unit опцию **Runtime/Sidecars autoupdate**:

    ![sidecars-autoupdate](../../../_assets/concepts/sidecars-autoupdate.png)

- Dctl

  Указать в [спецификации](https://a.yandex-team.ru/arc_vcs/yp/yp_proto/yp/client/api/proto/stage.proto?rev=9709368976789150745deccc5fac0cc79f560ea9#L240) Deploy Unit:
  
    Пример спецификации:
    
    ```yaml
      deploy_units:
        deployUnit:	    deployUnit:
          ...
          infra_components:
            allow_automatic_updates: true
    ```

{% endlist %}
