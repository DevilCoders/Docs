## Файл plugins/config.yaml
У каждой группы правил свой файл. В нем хранится следующая информация:

* `responsible` *required* - ответственные за эту группу правил. Первая команда в этом списке будет являться владельцами правил,
и будет иметь права на ОКи драфтов, а также должна мониторить свои правила самостоятельно.  (подробнее см. [responsible](responsible.md))
* `namespace` *required* - параметр, который определяет, к какому пространству имен принадлежит
данная группа правил. Возможные на данный момент опции можно посмотреть
[здесь](https://a.yandex-team.ru/arc_vcs/taxi/dmp/dwh/replication_rules/replication_rules/plugins/config.yaml#L144).
Нужен для того, чтобы отделить большие группы правил друг от друга.
* `secrets` - описание используемых группой правил секретов. Подробнее можно
посмотреть [здесь](secrets.md).

Также здесь может быть указан YT префикс - [YT prefixes](yt_prefixes.md)

Пример файла config.yaml:
```yaml
responsible:
  - taxidata_control
yt:
   prefix: taxi
namespace: taxi
secrets:
    secret_yav_alias:
        type: yav
        id:
            testing: sec-1234
            production: sec-4321
    STRONGBOX_ID:
        type: strongbox
        id: STRONGBOX_ID
```

## Глобальный файл plugins/config.yaml
Данный файл находится [здесь]({{ link_to_default_flaky_yaml }}) и он используется всеми группами правил.
В нем хранится следующая информация:
* `yt` - настройки по умолчанию, используемые при работе с YT.
    * `prefix` - префикс, используемый по умолчанию.
* `yt_prefixes` - описание всех доступных YT префиксов. Подробнее про YT префиксы можно прочитать [здесь](yt_prefixes.md)
* `namespaces` - описание всех доступных пространств имен.

### Пространства имен
Новое пространство имен можно задать как в глобальном файле `plugins/config.yaml`, так и в локальном(в этом случае оно будет доступно только данной группе правил).
Для заведения нового пространства имен необходимо указать его имя и определить для него следующие параметры:
* `resources` — ресурсы, используемые этим пространством имен.
    * `yt_prefix_aliases` - список доступных данному пространству имен YT префиксов, указанных в `yt_prefixes`.
    * `queue_mongo_aliases` - список доступных данному пространству имен очередей.
* `generator_hints` - параметры используемые тулзой генерации.
    * `expected_rule_name_prefixes` - список ожидаемых префиксов имен правил (используются для автоматического определения пространства имен).
    * `raw_yt_prefix` - YT префикс для raw слоя (должен быть одним из `yt_prefix_aliases`).
    * `raw_yt_default` - если `true` то по умолчанию будет генерироваться raw слой (может быть изменено через опцию `--force-raw` в тулзе генерации).
    * `default_queue_mongo` - очередь, используемая данным пространством имен по умолчанию (должна быть одной из `queue_mongo_aliases`).

Пример задания пространства имен для taxi:
```yaml
namespaces:
    taxi:
      resources:
        yt_prefix_aliases:
          - taxi
          - taxi-dwh
        queue_mongo_aliases:
          - replication_queue_mdb_1
      generator_hints:
          expected_rule_name_prefixes:
            - taxi
          raw_yt_prefix: taxi-dwh
          raw_yt_default: false
          default_queue_mongo: replication_queue_mdb_1
```
