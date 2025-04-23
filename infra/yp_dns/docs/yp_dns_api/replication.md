# Применение и репликация изменений

В данном разделе рассматривается путь запроса на изменение DNS записи через YP DNS API.
Эта страница содержит множество технических деталей, о которых пользователю _почти_ никогда не надо задумываться.

Верхнеуровнево у запроса есть два этапа:

1. применение изменения в одном из кластеров,
2. репликация изменения на остальные кластеры.

Первый этап выполняет компонент системы YP DNS API под названием **Bridge** (Бридж).
Он занимается непосредственно обработкой пользовательских запросов: применение изменений к записям, листинг зон, создание/удаление динамических зон.
Вторым этапом занимается второй компонент системы – **Replicator** (Репликатор).
Этот компонент выполняет фоновую работу и с пользователем никак не взаимодействует.

## Применение изменений (Bridge)

### Запрос

Для начала посмотрим, как выглядит запрос на изменение записи, который приходит от пользователя в Bridge:

```json
{
    "update": {
        "fqdn": "abc.yandex.test",
        "type": "AAAA",
        "data": "2a02:6b8:0:2b04:ff:ffff:a0e:fd47"
    }
}
```

Этот запрос добавляет или обновляет (если такая уже есть) запись типа `AAAA` для домена `abc.yandex.test` с контентом `2a02:6b8:0:2b04:ff:ffff:a0e:fd47`.
Допустим, такой записи для домена `abc.yandex.test` еще не существует, поэтому это запрос на добавление такой записи.

### Определение зоны {#find-zone}

Чтобы выполнить этот запрос `Bridge` сначала определяет зону, к которой относится домен `abc.yandex.test`, указанный в `fqdn`.
Это нужно сделать для двух вещей:

1. Определить в каких YP-кластерах находится зона.
Список кластеров записан в [конфиге зоны](https://a.yandex-team.ru/arc/trunk/arcadia/infra/libs/yp_dns/zone/protos/config.proto?rev=r9040922#L55).
2. Выставить лейбл `/labels/zone` новому DNS record set-у.
[TODO: ссылка: зачем это нужно].

Чтобы определить зону, Бридж последовательно отрезает по лейблу от изначального `fqdn` (домен может пройти такой путь: `abc.yandex.test` -> `yandex.test` -> `test` -> `.`) и на каждом шаге пытается найти зону с таким именем в списке зон.

{% cut "Откуда Бридж берет список зон?" %}

Из двух мест:

- Конфиги части зон указаны явно в [конфиге Бриджа](https://a.yandex-team.ru/arc/trunk/arcadia/infra/yp_dns_api/config/bridge_prod_config.json?rev=r8985258#L1768).
Это так называемые статические зоны.
- Остальные зоны – динамические.
Их конфиги хранятся в YP, в кластере YP-XDC, в объектах [типа `dns_zone`](https://a.yandex-team.ru/arc/trunk/arcadia/yp/yp_proto/yp/client/api/proto/dns_zone.proto).
Бридж периодически перезапрашивает этот список.

{% endcut %}

Если соответствующей зоны для `fqdn` не нашлось, то пользователю отдается ответ со [статусом `UNKNOWN_ZONE`](https://a.yandex-team.ru/arc/trunk/arcadia/infra/yp_dns_api/bridge/api/api.proto?rev=r8868826#L41).

### Выбор YP кластера для записи изменения

Итак, мы определили зону и узнали из ее конфига список YP кластеров, в которых она находится.
Но Бридж **не** применяет изменение в каждом кластере из этого списка.
Вместо этого он делает изменение только в одном, а Репликатор затем это изменение "доприменяет" в остальных.

Выбор кластера сейчас устроен таким образом, чтобы пессимизировать кластеры, при взаимодействии с которыми последнее время происходили ошибки,
и давать приоритет кластерам, которые успешно выполняют запросы от Бриджа. Выдержка из [кода](https://a.yandex-team.ru/arcadia/infra/yp_dns_api/bridge/cluster_scoring/scoring.h?rev=r9241592#L104) с описанием итогого порядка кластеров:

{% code '/infra/yp_dns_api/bridge/cluster_scoring/scoring.h' lang='cpp' lines='[BEGIN EScoreAlgorithm::PessimizeWithFails]-[END EScoreAlgorithm::PessimizeWithFails]' %}

После того как список кластеров зафиксирован, Бридж по порядку пробует применить изменение в каждом кластере.
Как только изменение успешно выполнено в каком-то кластере, Бридж отдает пользователю ответ об успехе, записывая туда имя этого кластера в [поле `cluster`](https://a.yandex-team.ru/arc/trunk/arcadia/infra/yp_dns_api/bridge/api/api.proto?rev=r8868826#L49).

### Применение изменения в кластере

Пусть мы выбрали кластер `YP-A` для попытки применить изменение.
Дальше нам надо узнать текущее значение record set-а `abc.yandex.test`.
Его мы получаем из локальной реплики данных кластера `YP-A`, которую мы храним и обновляем на диске, или непосредственно через get-запрос в YP, если локальная реплика [сильно отстала](https://a.yandex-team.ru/arc/trunk/arcadia/infra/yp_dns_api/bridge/config/config.proto?rev=r8229136#L35).

В начале мы договорились, что записи, которую мы хотим добавить, в record set-е нет.
То есть например, полученный record set выглядит так:

```json
{
    "meta": {
        "id": "abc.yandex.test"
    },
    "spec": {
        "records": [
            {
                "type": "AAAA",
                "data": "2a02:6b8:b010:c010:00ff:ffff:a02:fee2",
                "class": "IN",
                "ttl": 600
            }
        ]
    }
}
```

Получается, что применение изменения в рассматриваемом нами случае заключается в добавлении записи `AAAA 2a02:6b8:0:2b04:ff:ffff:a0e:fd47` в `/spec/records`.
Так что итоговый record set будет выглядеть так:

```json
{
    "meta": {
        "id": "abc.yandex.test"
    },
    "spec": {
        "records": [
            {
                "type": "AAAA",
                "data": "2a02:6b8:b010:c010:00ff:ffff:a02:fee2",
                "class": "IN",
                "ttl": 600
            },
            {
                "type": "AAAA",
                "data": "2a02:6b8:0:2b04:ff:ffff:a0e:fd47",
                "class": "IN",
                "ttl": 600
            }
        ]
    }
}
```

Но это не все.
Просто поменять список записей (`/spec/records`) недостаточно, так как Репликатор потом никак не сможет определить, что эту запись надо применить на остальные кластеры.
Поэтому мы помимо изменения списка записей, добавляем еще запись об изменении в `changelist`, который хранится в лейблах record set-а:

```json
{
    "meta": {
        "id": "abc.yandex.test"
    },
    "spec": {
        ...
    },
    "labels": {
        "zone": "yandex.test",
        "changelist": {
            "version": 1,
            "changes": [
                {
                    "uuid": "b69f3df8-956af899-9acd944e-5bef816a",
                    "timestamp": 1643223281117987,
                    "replicated": false,
                    "record_update_request": {
                        "content": {
                            "type": 28,  // AAAA
                            "data": "2a02:6b8:0:2b04:ff:ffff:a0e:fd47",
                            ...
                        },
                        "type": 1  // 1 – UPDATE, 2 – REMOVE
                    }
                }
            ]
        }
    }
}
```

Также инкрементируется счетчик `/labels/changelist/version`, он нужен для алгоритма репликации, но об этом позже.
Подробное описание структуры списка изменений можно найти [ниже](#changelist).
Также выставляем `/labels/zone`, если его там еще нет.

Таким образом нужно выполнить обновление сразу нескольких атрибутов record set-а: `/spec/records`, `/labels/changelist`, `/labels/zone` (если нужно). Это делается через запрос [`UpdateObjects`](https://wiki.yandex-team.ru/yp/api/#metodupdateobjects) к YP.
Но может использоваться [`CreateObjects`](https://wiki.yandex-team.ru/yp/api/#metodcreateobjects) – когда объект с `/meta/id == <fqdn>` в кластере не существует и к нему применяются изменения, причем как при изменениях типа update, так и (что важно) при изменениях типа remove (нужно для корректности).

## Репликация изменений (Replicator)

Здесь будет описание, а пока читайте код: [ReplicateChanges](https://a.yandex-team.ru/arcadia/infra/libs/yp_dns/replication/merge.h?rev=r9456111#L41).

## Структура списка изменений (Changelist) {#changelist}

Список изменений, который записывается в `/labels/changelist`, описывается [Protobuf-сообщением](https://a.yandex-team.ru/arcadia/infra/libs/yp_dns/changelist/proto/changelist.proto):

{% code '/infra/libs/yp_dns/changelist/proto/changelist.proto' lang='protobuf' lines='[BEGIN TChangelist]-[END TChangelist]' %}

В поле `changes` непосредственно хранится этот список изменений. Каждая из записей об изменении описывается таким Protobuf-сообщением:

{% code '/infra/libs/yp_dns/changelist/proto/changelist.proto' lang='protobuf' lines='[BEGIN TChange]-[END TChange]' %}

У `TChange` есть как мета-поля `uuid`, `timestamp`, `replicated`, которые не относятся непосредственно к физике самого изменения,
так и поля, которые задают тип изменения и его параметры, в `oneof Change`.

Например, сообщение, которое описывает изменение или удаление записи, выглядит следующим образом:

{% code '/infra/libs/yp_dns/changelist/proto/changelist.proto' lang='protobuf' lines='[BEGIN TRecordUpdateRequest]-[END TRecordUpdateRequest]' %}
