# Переотправка ресурсов баннера в новый транспорт в БК

Отправка делается ваншотом [BannerResourcesResyncOneshot](https://a.yandex-team.ru/arc/trunk/arcadia/direct/oneshot/src/main/java/ru/yandex/direct/oneshot/oneshots/bsexport/resources/BannerResourcesResyncOneshot.kt?rev=r7671509#L74)

В качестве параметра он принимает json c именем кластера и путем к таблице, в которой лежат данные для переотправки.  
Пример параметра:
```json
{"tablePath": "//home/direct/tmp/mspirit_development/resendResources", "ytCluster": "HAHN"}
```

Таблица с данными должна иметь колонки **bid** и **resource_type**.  
В первой записываются директовые id-ники баннера для переотправки, во второй записывается, какие ресурсы баннера нужно переотправить.

Возможные типы ресурсов хранятся в [enum'е](https://a.yandex-team.ru/arc/trunk/arcadia/direct/apps/event-sourcing-system/config/src/main/java/ru/yandex/direct/ess/logicobjects/bsexport/resources/BannerResourceType.java?rev=r7673417#L3).
Если нужно переотправить все ресуры баннера — указать `ALL`.

## Как запустить ваншот
Для запуска ваншота нужна роль в Директе developer, ее можно запросить у [Пети Сивкова](https://staff.yandex-team.ru/sivkov) или у любого, у кого есть роль `SUPER` в продакшене. Роль выдается на существующий логин суперридера

1. Создать запуск на странице [Ваншоты](https://direct.yandex.ru/internal_tools/#oneshots).
   Выбрать в списке `~.bsexport.resources.BannerResourcesResyncOneshot` и указать параметры запуска
1. Выбрать кого-нибудь из колонки **Апруверы** и попросить подтвердить запуск ваншота
1. На странице [запуска ваншотов](https://direct.yandex.ru/internal_tools/#oneshot_launches) выбрать свой и запустить.
    Логи запуска можно смотреть перейдя по ссылке в колонке **Лог**

Подробнее про ваншоты можно почитать в разделе [про ваншоты](../oneshot/concept.md)

### Ограничения

Так как отправка баннеров происходит через ESS, большое количество баннеров может сильно нагрузить работу всего ESS.
Поэтому баннеры отправляются чанками, между каждым чанком перерыв на некоторое время. Эти величины задаются в базе в таблице ppc_properties.

Изменять их можно на [странице внутренних инструментов](https://direct.yandex.ru/internal_tools/#set_typed_ppc_property).  
Названия пропертей `resync_banner_resources_chunk_size`, `resync_banner_resources_rerlax_time`.

При отправке большого количества баннеров(порядка 1_000_000) эти величины стоит регулировать, наблюдая за общим состоянием ess-цепочки, например, на [дашборде](https://solomon.yandex-team.ru/?project=direct&dashboard=ess&project=direct&cluster=app_binlogbroker&service=java-monitoring&env=production)
