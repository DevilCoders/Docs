# Juggler subagent

Описывается, как запустить в своих подах [juggler](https://wiki.yandex-team.ru/sm/juggler/) subagent.

## Настройка в dctl {#setup-dctl}

Для запуска juggler subagent в конкретном box нужно внести его в поле `TDeployUnitSpec.box_juggler_configs` в [спеке stage](https://a.yandex-team.ru/arc/trunk/arcadia/yp/yp_proto/yp/client/api/proto/stage.proto).

Ресурсы проверок (bundle) описываются в `archived_checks`. [Как собрать свой bundle с проверками.](https://wiki.yandex-team.ru/sm/juggler/juggler-client/#sborkasvoegobandla)

Также нужно добавить описание агента в `pod_template_spec.spec.host_infra.monitoring.juggler_subagents`, чтобы хостовый juggler знал, где искать субагент.

## Что происходит внутри {#inside}

В каждом указанном box поднимается workload с juggler subagent и указанным в конфигурации набором проверок.

## Требования по ресурсам {#resources}

**Для каждого box c juggler subagent** в Поде будут запрошены дополнительные ресурсы:

* 512 МБ диска.
* 256 МБ RAM.
* 0.13 ядра CPU.

Сумма этих ресурсов будет прибавлена к запрашиваемым ресурсам Пода.

## История изменений {#changelog}

Есть два вида ченджлога: один касается версии самого сайдкара, а другой — внешних его настроек (на базе runtime version).

### Изменения runtime version {#changelog-runtime}

* В [runtime version №2](../../../reference/patchers-revision.md#new-runtime-version-2) исправлено выставление дисковой квоты на juggler workload. Теперь выставляется [512MB HDD на каждый box](sidecars.md#quotas).

* С версии [runtime version №2](../../../reference/patchers-revision.md#new-runtime-version-2) при включенном juggler у пода выставляется persistent fqdn вместо transient. 

* С [runtime version №3](../../../reference/patchers-revision.md#new-runtime-version-3) добавлена поддержка нескольких juggler bundle.

* В [runtime version №6](../../../reference/patchers-revision.md#new-runtime-version-6) добавлена [возможность сбора портометрик](../../../reference/patchers-revision.md#new-runtime-version-6) с системных сайдкаров.

* В [runtime version №7](../../../reference/patchers-revision.md#new-runtime-version-7) изменилась логика приноса системных папок и вольюмов для writable папок в случае использования read only fs бокса. 

* С [runtime version №10](../../../reference/patchers-revision.md#new-runtime-version-10) скрипт инициализации Juggler теперь падает при неуспешной распаковке ресурсов и других ошибках.