# pod_patcher

Можно использовать для массового обновления всех подов на кластере.

## Описание

Скрипт итерируется по заданным кластерам и берет все pod, соответствующие фильтру `filter` (синтаксис как у обычных запросов в yp).

Для выбора подов под `deploy` надо смотреть на `[/labels/deploy_engine]`.

Сейчас скрипт просто выбирает эти поды, но ничего с ними не делает. Для обновлений надо дописать код [вот сюда](https://a.yandex-team.ru/arc/trunk/arcadia/infra/deploy/dri/pod_patcher/__main__.py?rev=6015579#L89-92).

Продакшн лучше обновлять аккуратно - по частям. Например, фильтром вроде `-f '[/meta/id] >= "a" and [/meta/id] < "b"'`.

## Пример использования

Для [SPI](https://st.yandex-team.ru/SPI-8369) надо было всем подам проставить `mock_label`.

Для этого скрипт был изменен вот так:

```
def update_pod_custom(yp_client_stub, transaction_id, pod):
    req = object_service_pb2.TReqUpdateObject()
    req.object_type = data_model.OT_POD
    req.object_id = pod

    req.transaction_id = transaction_id

    upd = req.set_updates.add()
    upd.path = "/labels/spi-8369-mock-label"
    upd.value = "mock"

    yp_client_stub.UpdateObject(req)
```

Запускался вот так:

```
$ date && YP_TOKEN=<> ./pod-patcher -f "([/labels/deploy_engine]='RSC' or [/labels/deploy_engine]='MCRSC') and [/status/agent/execution_error/code]=1" --select-limit 200 vla
Wed Nov  6 21:46:49 MSK 2019
--------------------------------------------------
Update cluster vla
Use yp token from env YP_TOKEN
Current pod filter '([/labels/deploy_engine]='RSC' or [/labels/deploy_engine]='MCRSC') and [/status/agent/execution_error/code]=1'
You select 93 pods
This is a lot of objects, you really want to continue? If yes type 'Yes, do as I say!': Yes, do as I say!
Current pods:
dff7ny5gnht7sis5, v2hyvevmb2imtlym, <...>,  b6vyeiwwsy4yuljx

<debug info>

```
