### Platinum
Изолированный кластер из (примерно) 900 машин **без ssd** (_как определяется этот список?_).
Шард поднимается в память целиком. Сожительства нет, машины полностью под управлением YP.

### base
Сервис: https://nanny.yandex-team.ru/ui/#/services/catalog/web_platinum_base/

Поды размечены двумя видами меток (номера шардов совпадают):
```json
{
    "shard_id": "primus-PlatinumTier0-0-1-0000000000",
    "gencfg.shard": "PlatinumTier0-0-1"
}
```
`/labels/shard_id` – предпочтительная схема, `/labels/gencfg.shard` – устаревшая.

Прод слушает на порту 80, хамстер – на 8000.

Discovery базовых выполняется с помощью endpoint set-ов вида `web-platinum-base-shard-105`,
использующих устаревшую схему маркировки подов:
```json
{
    "pod_filter": "([/labels/gencfg.shard] = 'PlatinumTier0-0-105') AND [/meta/pod_set_id] = 'web-platinum-base'",
    "protocol": "TCP",
    "port": 80
}
```
Заведены и другие endpoint set-ы:
```
web_platinum_base.primus-PlatinumTier0-0-105-0000000000
web_platinum_base.primus-PlatinumTier0-0-105-0000000000.hamster
web-platinum-base.105.hamster
```
Все эти разновидности в фильтре ссылаются на `/labels/shard_id`.
В endpoint set-ах вида `.hamster` указан порт хамстера:
```json
{
    "pod_filter": "([/labels/shard_id] = 'primus-PlatinumTier0-0-105-0000000000') AND [/meta/pod_set_id] = 'web-platinum-base'",
    "protocol": "TCP",
    "port": 8000
}
```

### int
Сервис: https://nanny.yandex-team.ru/ui/#/services/catalog/web_platinum_int/

Используется один (устаревший) вид меток:
```json
{
    "gencfg.shard": "PlatinumTier0-int-0-5"
}
```
Endpoint set-ы имеют вид `web-platinum-int-5`
```json
{
    "pod_filter": "([/labels/gencfg.shard] = \"PlatinumTier0-int-0-5\") AND [/meta/pod_set_id] = \"web-platinum-int\"",
    "protocol": "TCP",
    "port": 80
}
```
### int hamster
Сервис: https://nanny.yandex-team.ru/ui/#/services/catalog/web_platinum_int_hamster/

Для discovery базовых используются endpoint set-ы вида `web-platinum-base.105.hamster`
Используется один вид меток (названия меток "новые", значения аналогичны проду)
```json
{
    "shard_id": "PlatinumTier0-int-0-5"
}
```
Endpoint set-ы имеют вид `web-platinum-int-hamster.5`:
```json
{
    "pod_filter": "([/labels/shard_id] = \"PlatinumTier0-int-0-5\") AND [/meta/pod_set_id] = \"web-platinum-int-hamster\"",
    "protocol": "TCP",
    "port": 80
}
```
Конфиги получают имена `web-platinum-int-hamster.PlatinumTier0-int-0-5.cfg`,
таким образом везде используется один и тот же идентификатор "шарда".

### покрыто мраком
Для генерации конфигов прода используется интлукап, построенный на группах псевдохостов.

#### Tier1
_TBD_
