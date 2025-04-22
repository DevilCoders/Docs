# API для управления DNS записями в YP

## Адрес

- `dns-api-bridge.yp.yandex.net`

- HTTP порт `8080`, gRPC порт `8081`

## Протокол работы

Поддерживаются протоколы gRPC и HTTP.

### Ручки

Путь | Описание | gRPC | HTTP
:--- | :--- | :--- | :---
`/ping` | | `Ping` | GET-запрос
`/records/update`             | [Добавление/обновление/удаление записей](#update-records)    | `UpdateRecords`      | POST-запрос. Запрос-ответ: `TReqUpdateRecords-TRspUpdateRecords` в сериализованном виде
`/records/update/json`        | [Добавление/обновление/удаление записей](#update-records)    | -                    | POST-запрос. Запрос-ответ: `TReqUpdateRecords-TRspUpdateRecords` в формате json
`/list_zone_record_sets`      | [Получить список record set-ов зоны](#list-zone-record-sets) | `ListZoneRecordSets` | POST-запрос. Запрос-ответ: `TReqListZoneRecordSets-TRspListZoneRecordSets` в сериализованном виде
`/list_zone_record_sets/json` | [Получить список record set-ов зоны](#list-zone-record-sets) | -                    | POST-запрос. Запрос-ответ: `TReqListZoneRecordSets-TRspListZoneRecordSets` в формате json
`/zones/list`       | [Получить список зон для своего сервиса](#list-zones) | `ListZones`  | POST-запрос. Запрос-ответ: `TReqListZones-TRspListZones` в сериализованном виде
`/zones/list/json`  | [Получить список зон для своего сервиса](#list-zones) | -            | POST-запрос. Запрос-ответ: `TReqListZones-TRspListZones` в формате json
`/zone/create`      | [Создать новую зону](#create-zone)                    | `CreateZone` | POST-запрос. Запрос-ответ: `TReqCreateZone-TRspCreateZone` в сериализованном виде
`/zone/create/json` | [Создать новую зону](#create-zone)                    | -            | POST-запрос. Запрос-ответ: `TReqCreateZone-TRspCreateZone` в формате json
`/zone/remove`      | [Удалить зону](#remove-zone)                          | `RemoveZone` | POST-запрос. Запрос-ответ: `TReqRemoveZone-TRspRemoveZone` в сериализованном виде
`/zone/remove/json` | [Удалить зону](#remove-zone)                          | -            | POST-запрос. Запрос-ответ: `TReqRemoveZone-TRspRemoveZone` в формате json

Структура запросов и ответов описана в файлах [arcadia/infra/yp_dns_api/bridge/api/api.proto](http://a.yandex-team.ru/arc/trunk/arcadia/infra/yp_dns_api/bridge/api/api.proto) (работа с записями) и [arcadia/infra/libs/yp_dns/dynamic_zones/zones_manager_service/api/api.proto](http://a.yandex-team.ru/arc/trunk/arcadia/infra/libs/yp_dns/dynamic_zones/zones_manager_service/api/api.proto) (работа с зонами)

## UpdateRecords {#update-records}

Метод позволяет изменять DNS записи.

Есть два типа изменения: обновление и удаление записи. Обновление подразумевает создание записи, если ее до этого не существовало.
Важный момент заключается в том, как выбирается запись, к которой относится запрашиваемое изменение:

1. Если это запись типа `SOA`, то ключом для сравнения является пара `key(record) = (fqdn, type) == (fqdn, SOA)`. То есть запросы с `type=SOA` будут применяться ко всем `SOA` записям зоны.
2. Для остальных записей ключом является `key(record) = (fqdn, type, data)`.

Таким образом, изменение применяется ко всем записям, для которых `key(record) == key(update)`. По-хорошему, такая запись всегда одна. Разберем на примерах:

{% cut "Пример 1: обновление SOA" %}
Допустим есть record set:

```json
{
  "meta": {"id": "zone.yandex.net"},
  "spec": {
    "records": [
      {"type": "NS", "data": "ns3.yandex.ru.", "class": "IN", "ttl": 172800},
      {"type": "NS", "data": "ns4.yandex.ru.", "class": "IN", "ttl": 172800},
      {
        "type": "SOA",
        "data": "ns3.yandex.ru. sysadmin.yandex.ru. 2019012931 900 600 3600000 300",
        "class": "IN",
        "ttl": 600
      }
    ]
  }
}
```

У него есть три записи: две `NS` и одна `SOA`. Обозначим их за `record[0]`, `record[1]`, `record[2]`. Мы хотим поменять `primary nameserver` в `SOA` записи с `ns3.yandex.ru` на `ns4.yandex.net`. Для этого мы составляем такой запрос:

```json
{
  "requests": [
    {
      "update": {
        "fqdn": "zone.yandex.net",   // совпадает с /meta/id record set-а
        "type": "SOA",               // тип записи
        "data": "ns4.yandex.net. sysadmin.yandex.ru. 2019012931 900 600 3600000 300" // контент записи
      }
    }
  ]
}
```

Тогда Бридж сделает следующее на такой запрос:

1. Найдет record set с `[/meta/id] == "zone.yandex.net"`.
2. Найдет записи, которые относятся к этому изменению. Для этого он сравнит `key(update) = ("zone.yandex.net", SOA)` с `key(record[i]), i = 0..2`:
2.1. `key(record[0]) = ("zone.yandex.net", NS, "ns3.yandex.ru.") != ("zone.yandex.net", SOA)` – не подходит
2.2. `key(record[1]) = ("zone.yandex.net", NS, "ns4.yandex.ru.") != ("zone.yandex.net", SOA)` – не подходит
2.3. `key(record[2]) = ("zone.yandex.net", SOA) == ("zone.yandex.net", SOA)` – подходит!
3. Сматчилась третья запись, т.к. она тоже `SOA`, этого достаточно. Поэтому для нее применится изменение: `data` станет равной `ns4.yandex.net. sysadmin.yandex.ru. 2019012931 900 600 3600000 300`.

Итоговый record set будет выглядеть так:

```json
{
  "meta": {"id": "zone.yandex.net"},
  "spec": {
    "records": [
      {"type": "NS", "data": "ns3.yandex.ru.", "class": "IN", "ttl": 172800},
      {"type": "NS", "data": "ns4.yandex.ru.", "class": "IN", "ttl": 172800},
      {
        "type": "SOA",
        "data": "ns4.yandex.ru. sysadmin.yandex.ru. 2019012931 900 600 3600000 300",
        "class": "IN",
        "ttl": 600
      }
    ]
  }
}
```

Но что если `SOA` записи не было бы в record set-е? Тогда бы она создалась исходя из данных в запросе. Об этом в следующем примере.

{% endcut %}

{% cut "Пример 2: создание SOA" %}
Допустим есть record set:

```json
{
  "meta": {"id": "zone.yandex.net"},
  "spec": {
    "records": [
      {"type": "NS", "data": "ns3.yandex.ru.", "class": "IN", "ttl": 172800},
      {"type": "NS", "data": "ns4.yandex.ru.", "class": "IN", "ttl": 172800}
    ]
  }
}
```

У него есть две записи типа `NS`. Обозначим их за `record[0]`, `record[1]`. Мы хотим к ним добавить `SOA` запись с `ttl = 600` и `data = "ns3.yandex.net. sysadmin.yandex.ru. 2019012931 900 600 3600000 300"`. Для этого мы составляем такой запрос:

```json
{
  "requests": [
    {
      "update": {
        "fqdn": "zone.yandex.net",   // совпадает с /meta/id record set-а
        "type": "SOA",               // тип записи
        "ttl": 600,                  // ttl записи
        "data": "ns3.yandex.net. sysadmin.yandex.ru. 2019012931 900 600 3600000 300" // контент записи
      }
    }
  ]
}
```

Тогда Бридж сделает следующее на такой запрос:

1. Найдет record set с `[/meta/id] == "zone.yandex.net"`.
2. Найдет записи, которые относятся к этому изменению. Для этого он сравнит `key(update) = ("zone.yandex.net", SOA)` с `key(record[i]), i = 0..2`:
2.1. `key(record[0]) = ("zone.yandex.net", NS, "ns3.yandex.ru.") != ("zone.yandex.net", SOA)` – не подходит
2.2. `key(record[1]) = ("zone.yandex.net", NS, "ns4.yandex.ru.") != ("zone.yandex.net", SOA)` – не подходит
3. Не подошла ни одна запись, поэтому Бриджу придется ее создать.
Итоговый record set будет выглядеть так:

```json
{
  "meta": {"id": "zone.yandex.net"},
  "spec": {
    "records": [
      {"type": "NS", "data": "ns3.yandex.ru.", "class": "IN", "ttl": 172800},
      {"type": "NS", "data": "ns4.yandex.ru.", "class": "IN", "ttl": 172800},
      {
        "type": "SOA",
        "data": "ns3.yandex.ru. sysadmin.yandex.ru. 2019012931 900 600 3600000 300",
        "class": "IN",
        "ttl": 600
      }
    ]
  }
}
```

{% endcut %}

{% cut "Пример 3: удаление SOA" %}>

Допустим есть record set:

```json
{
  "meta": {"id": "zone.yandex.net"},
  "spec": {
    "records": [
      {"type": "NS", "data": "ns3.yandex.ru.", "class": "IN", "ttl": 172800},
      {"type": "NS", "data": "ns4.yandex.ru.", "class": "IN", "ttl": 172800},
      {
        "type": "SOA",
        "data": "ns3.yandex.ru. sysadmin.yandex.ru. 2019012931 900 600 3600000 300",
        "class": "IN",
        "ttl": 600
      }
    ]
  }
}
```

У него есть три записи: две `NS` и одна `SOA`. Обозначим их за `record[0]`, `record[1]`, `record[2]`. Мы хотим удалить `SOA` запись.
Т.к. ключом для `SOA` записи является только `fqdn` и `type`, то достаточно составить такой запрос:

```json
{
  "requests": [
    {
      "remove": {
        "fqdn": "zone.yandex.net",   // совпадает с /meta/id record set-а
        "type": "SOA",               // тип удаляемой записи
        "data": "abracadabra"        // data не имеет значения, может быть опущено,
                                     //   т.к. не входит в ключевое поле для SOA
      }
    }
  ]
}
```

Тогда Бридж попробует сделать следующее:

1. Найдет record set с `[/meta/id] == "zone.yandex.net"`.
2. Найдет записи, которые относятся к этому изменению. Для этого он сравнит `key(update) = ("zone.yandex.net", SOA)` с `key(record[i]), i = 0..2`:
2.1. `key(record[0]) = ("zone.yandex.net", NS, "ns3.yandex.ru.") != ("zone.yandex.net", SOA)` – не подходит
2.2. `key(record[1]) = ("zone.yandex.net", NS, "ns4.yandex.ru.") != ("zone.yandex.net", SOA)` – не подходит
2.3. `key(record[2]) = ("zone.yandex.net", SOA) == ("zone.yandex.net", SOA)` – подходит!
3. Сматчилась третья запись, т.к. она тоже `SOA`, этого достаточно. Т.к. запрос у нас на удаление, то запись удалится.

Итоговый record set будет выглядеть так:

```json
{
  "meta": {"id": "zone.yandex.net"},
  "spec": {
    "records": [
      {"type": "NS", "data": "ns3.yandex.ru.", "class": "IN", "ttl": 172800},
      {"type": "NS", "data": "ns4.yandex.ru.", "class": "IN", "ttl": 172800}
    ]
  }
}
```

{% endcut %}

{% cut "Пример 4: обновление записей других типов на примере AAAA" %}

TODO

{% endcut %}

{% note warning "Важное про CNAME записи" %}

Работа с записями с типом `CNAME` происходит особенным образом:

- Добавление `CNAME` записи **удаляет все** остальные записи для указанного `fqdn`.
- И наоборот, добавление записи *любого* другого типа **удаляет** все `CNAME` записи для этого `fqdn`.

Тикет на внедрение этого изменения: <https://st.yandex-team.ru/DISCOVERY-120>.

{% endnote %}

### Запрос

{% code '/infra/yp_dns_api/bridge/api/api.proto' lang='protobuf' lines='[BEGIN ERecordType]-[END ERecordType]' %}

{% code '/infra/yp_dns_api/bridge/api/api.proto' lang='protobuf' lines='[BEGIN TReqUpdateRecord]-[END TReqUpdateRecord]' %}

{% code '/infra/yp_dns_api/bridge/api/api.proto' lang='protobuf' lines='[BEGIN TReqRemoveRecord]-[END TReqRemoveRecord]' %}

{% code '/infra/yp_dns_api/bridge/api/api.proto' lang='protobuf' lines='[BEGIN THints]-[END THints]' %}

{% code '/infra/yp_dns_api/bridge/api/api.proto' lang='protobuf' lines='[BEGIN TRecordRequest]-[END TRecordRequest]' %}

{% code '/infra/yp_dns_api/bridge/api/api.proto' lang='protobuf' lines='[BEGIN TReqUpdateRecords]-[END TReqUpdateRecords]' %}

### Ответ

{% code '/infra/yp_dns_api/bridge/api/api.proto' lang='protobuf' lines='[BEGIN TRspUpdateRecord]-[END TRspUpdateRecord]' %}

{% code '/infra/yp_dns_api/bridge/api/api.proto' lang='protobuf' lines='[BEGIN TRspRemoveRecord]-[END TRspRemoveRecord]' %}

{% code '/infra/yp_dns_api/bridge/api/api.proto' lang='protobuf' lines='[BEGIN TRecordResponse]-[END TRecordResponse]' %}

{% code '/infra/yp_dns_api/bridge/api/api.proto' lang='protobuf' lines='[BEGIN TRspUpdateRecords]-[END TRspUpdateRecords]' %}

### Примеры

{% cut "Удаление и создание записи" %}

Контент файла `req.json`:

```json
{
  "requests": [
    {
      "remove": {
        "fqdn": "a.test-zone.yandex.net",
        "type": "AAAA",
        "data": "2a02:6b8:0:2b04:00ff:ffff:a0e:fd47"
      }
    },
    {
      "update": {
        "fqdn": "b.test-zone.yandex.net",
        "type": "AAAA",
        "data": "2a02:6b8:0:2b04:00ff:ffff:a0e:fd47",
        "ttl": 300
      }
    }
  ]
}
```

Запрос:

```sh
$ curl -X POST -d @req.json http://dns-api-bridge.yp.yandex.net:8080/records/update/json | jq .
{
  "responses": [
    {
      "remove": {
        "status": 1,
        "cluster": "sas-test"
      }
    },
    {
      "update": {
        "status": 1,
        "cluster": "sas-test"
      }
    }
  ]
}
```

Результат:

```sh
$ yp get dns_record_set --address sas-test b.test-zone.yandex.net --selector /meta --selector /spec --selector /labels
[
    {
        "effective_account_id" = #;
        "account_id" = "tmp";
        "inherit_acl" = %true;
        "creation_time" = 1592208278090449u;
        "acl" = [
            {
                "action" = "allow";
                "subjects" = [
                    "robot-ypdnsapi";
                ];
                "permissions" = [
                    "read";
                    "write";
                ];
            };
        ];
        "type" = "dns_record_set";
        "id" = "b.test-zone.yandex.net";
        "uuid" = "75495cb5-4b9ab059-cf21e679-555a2b4e";
    };
    {
        "records" = [
            {
                "data" = "2a02:6b8:0:2b04:00ff:ffff:a0e:fd47";
                "type" = "AAAA";
                "class" = "IN";
                "ttl" = 300u;
            };
        ];
    };
    {
        "zone" = "test-zone.yandex.net";
    };
]
```

{% endcut %}

## ListZoneRecordSets {#list-zone-record-sets}

Метод позволяет получить список record set-ов зоны.

Список record set-ов можно читать частями. Для этого нужно указать `limit` – максимальное число записей в ответе. В ответе будет передан `continuation_token`, его можно использовать в следующем запросе для получения следующей части данных.
Пагинация заканчивается, когда число record set-ов в ответе меньше чем `limit`.
Важно понимать, что в этом случае консистентность данных не гарантируется. Данные консистентны в рамках одного запроса, но не в рамках всей цепочки запросов.

Список record set-ов в ответе упорядочен лекcикографически по `id`.

### Запрос TReqListZoneRecordSets

{% code '/infra/yp_dns_api/bridge/api/api.proto' lang='protobuf' lines='[BEGIN TReqListZoneRecordSets]-[END TReqListZoneRecordSets]' %}

### Ответ TRspListZoneRecordSets

{% code '/infra/yp_dns_api/bridge/api/api.proto' lang='protobuf' lines='[BEGIN TRecord]-[END TRecord]' %}

{% code '/infra/yp_dns_api/bridge/api/api.proto' lang='protobuf' lines='[BEGIN TRecordSet]-[END TRecordSet]' %}

{% code '/infra/yp_dns_api/bridge/api/api.proto' lang='protobuf' lines='[BEGIN TRspListZoneRecordSets]-[END TRspListZoneRecordSets]' %}

### Примеры листинга record set-ов

{% cut "Листинг зоны с пагинацией' %}

```sh
$ curl -X POST -d '{"zone":"ipmi.yandex.net","limit":2}' http://dns-api-bridge.yp.yandex.net:8080/list_zone_record_sets/json | jq .
{
  "status": 1,
  "record_sets": [
    {
      "id": "00-0a-9c-60-e3-dc.ipmi.yandex.net",
      "records": [
        {
          "ttl": 799,
          "class": "IN",
          "type": "AAAA",
          "data": "2620:10f:d00b:1004:00ff:ffff:a1c:fcba"
        }
      ]
    },
    {
      "id": "00-0d-5d-0b-4f-4e.ipmi.yandex.net",
      "records": [
        {
          "ttl": 799,
          "class": "IN",
          "type": "AAAA",
          "data": "2a02:6b8:b010:c010:00ff:ffff:a01:fee2"
        }
      ]
    }
  ],
  "continuation_token": "MDAtMGQtNWQtMGItNGYtNGUuaXBtaS55YW5kZXgubmV0",
  "yp_timestamps": [
    {
      "key": "xdc",
      "value": 1732073299808092200
    }
  ]
}
$ curl -X POST -d '{"zone":"ipmi.yandex.net","limit":2,"continuation_token":"MDAtMGEtOWMtNjAtZTMtZGMuaXBtaS55YW5kZXgubmV0"}' http://dns-api-bridge.yp.yandex.net:8080/list_zone_record_sets/json | jq .
{
  "status": 1,
  "record_sets": [
    {
      "id": "00-0d-5d-0b-6b-52.ipmi.yandex.net",
      "records": [
        {
          "ttl": 799,
          "class": "IN",
          "type": "AAAA",
          "data": "2a02:6b8:b010:c010:00ff:ffff:a17:f22b"
        }
      ]
    },
    {
      "id": "00-0d-5d-0b-6b-6f.ipmi.yandex.net",
      "records": [
        {
          "ttl": 799,
          "class": "IN",
          "type": "AAAA",
          "data": "2a02:6b8:b010:c010:00ff:ffff:a10:ff4e"
        }
      ]
    }
  ],
  "continuation_token": "MDAtMGQtNWQtMGItNmItNmYuaXBtaS55YW5kZXgubmV0",
  "yp_timestamps": [
    {
      "key": "xdc",
      "value": 1732073357790151000
    }
  ]
}
```

{% endcut %}

## ListZones {#list-zones}

Метод позволяет получить список динамических зон в YP. Динамические зоны – это те, что созданы через Bridge (ручка `/zone/create[/json]`, зоны описанные в конфигах DNS-серверов тут не присутствуют.

В параметрах запроса нужно указать имя своего сервиса, от которого делается запрос (имя должно быть заранее зарегистрировано в Бридже). Это необходимо для того, чтобы правильно определить список зон, который Бридж должен отдать в ответе, т.к. для каждого сервиса этот список может быть свой ([подробнее](https://wiki.yandex-team.ru/ypdns/dynamic-zones-management/)).

### Запрос TReqListZones

{% code '/infra/libs/yp_dns/dynamic_zones/zones_manager_service/api/api.proto' lang='protobuf' lines='[BEGIN TReqListZones]-[END TReqListZones]' %}

Список возможных значений `service_type`:

{% code '/infra/libs/yp_dns/dynamic_zones/zones_state_coordinator.h' lang='cpp' lines='[BEGIN EServiceType]-[END EServiceType]' %}

### Ответ TRspListZones

{% code '/infra/libs/yp_dns/dynamic_zones/zones_manager_service/api/api.proto' lang='protobuf' lines='[BEGIN TReqListZones]-[END TReqListZones]' %}

{% code '/infra/libs/yp_dns/dynamic_zones/zones_manager_service/api/api.proto' lang='protobuf' lines='[BEGIN TZone]-[END TZone]' %}

{% code '/infra/libs/yp_dns/zone/protos/config.proto' lang='protobuf' lines='[BEGIN TZoneConfig]-[END TZoneConfig]' %}

{% code '/infra/libs/yp_dns/dynamic_zones/zones_manager_service/api/api.proto' lang='protobuf' lines='[BEGIN TRspListZones]-[END TRspListZones]' %}

### Примеры листинга зона

{% cut "Получение списка динамических зон" %}

```sh
$ curl -X POST -d '{"service_type":"BRIDGE"}' http://dns-api-bridge.yp.yandex.net:8080/zones/list/json -v | jq .
{
  "status": "OK",
  "zones": [
    {
      "config": {
        "Name": "test-zone-r3.yandex.net",
        "PrimaryNameserver": "ns1.yp-dns.yandex.net",
        "Nameservers": [
          "ns1.yp-dns.yandex.net",
          "ns2.yp-dns.yandex.net"
        ],
        "YPClusters": [
          "sas-test",
          "man-pre"
        ],
        "SelectRecordSetMode": "MERGE",
        "Owners": [
          "robot-ypdnsapi",
          "robot-ypdnsapi-repl"
        ]
      }
    }
  ]
}
```

{% endcut %}

## CreateZone {#create-zone}

Метод позволяет создать зону.

### Запрос TReqCreateZone

{% code '/infra/libs/yp_dns/dynamic_zones/zones_manager_service/api/api.proto' lang='protobuf' lines='[BEGIN TZone]-[END TZone]' %}

{% code '/infra/libs/yp_dns/zone/protos/config.proto' lang='protobuf' lines='[BEGIN TZoneConfig]-[END TZoneConfig]' %}

{% code '/infra/libs/yp_dns/dynamic_zones/zones_manager_service/api/api.proto' lang='protobuf' lines='[BEGIN TReqCreateZone]-[END TReqCreateZone]' %}

#### Конфиг зоны {#zone-config}

Подавляющее большинство полей конфига можно не указывать.
Ниже приведены наиболее важные из полей.

Поле | Обязательность | Рекомендуемое значение | Описание
:--- | :--- | :--- | :---
`Name` | required | [RFC 1035 2.3](https://www.ietf.org/rfc/rfc1035.txt) | Имя зоны, в нижнем регистре, без точки в конце.
`YPClusters` | optional | `["sas", "man", "vla"]` | Список имен YP-кластеров, где зона будет храниться. Если не указать, то используются "sas", "man", "vla".
`DefaultTtl` | optional | Не указывать | Дефолтное значение ttl при создании записи в зоне, если в запросе ttl явно не указан.
`Owners` | optional | Не указывать | Список логинов, которые будут указаны владельцами объектов в YP. Обычно не нужно.

Следующие опции задают значения, так называемой, *статической* `SOA` записи, которая будет генерироваться по дефолту.
Если при этом в YP есть `SOA` запись для зоны,
  например, она была загружена как отдельная запись через метод [UpdateRecords](#update-records) (такую будем называть *динамической*),
  то будет использоваться запись из YP (динамическая), а значения из конфига зоны, соответственно, будут игнорироваться.

Поле | Дефолт | Описание
:--- | :--- | :---
`PrimaryNameserver` | Нет, значение нужно указать | Имя главного авторитетного nameserver-а зоны
`Hostmaster` | `sysadmin.yandex-team.ru` | Email ответственного за зону
`SOARecordTtl` | 3600 | TTL записи
`SOASerial` | 0 | Serial number
`SOARecordMinimumTtl` | 120 | Negative TTL записи
`SOARefresh` | 900 | Refresh
`SOARetry` | 600 | Retry
`SOAExpire` | 604800 | Expire
`SerialGenerateMode` | `YP_TIMESTAMP_BASED` | Режим генерации serial number. `ORIGINAL` - число изменяется, `YP_TIMESTAMP_BASED` - генерируется на основе YP timestamp-ов.

{% note tip %}

Рекомендуется иметь одинаковые значения `SOA` записи в конфиге зоны и в записи в YP.

{% endnote %}

Следующий опции задают значения статических `NS` записей.
Аналогично `SOA` записи, `NS` записи с такими значениями будут генерироваться и отдаваться в ответе, если в YP нет отдельных `NS` записей.

Поле | Дефолт | Описание
:--- | :--- | :---
`Nameservers` | Нет, список нужно указать | Список nameserver-ов зоны
`Hostmaster` | `sysadmin.yandex-team.ru` | Email ответственного за зону
`NSRecordTtl` | 3600 | TTL записей

{% note tip %}

Рекомендуется иметь одинаковый список `NS` записей в конфиге зоны и `NS` записей в YP.

{% endnote %}

Про остальные опции знать скорее всего не нужно, только если вы не хотите что-то специфичное.
Про эти опции можно узнать у разработчиков YP DNS или почитать код.

Таким образом, важно указать: `Name`, опции `SOA` записи и опции `NS` записей.

### Ответ TRspCreateZone

{% code '/infra/libs/yp_dns/dynamic_zones/zones_manager_service/api/api.proto' lang='protobuf' lines='[BEGIN TRspCreateZone]-[END TRspCreateZone]' %}

### Примеры создания зоны

{% cut "Создание динамической зоны" %}

Контент файла `req.json`:

```json
{
    "zone": {
        "config": {
            "Name": "test-zone.yandex.net",
            "PrimaryNameserver": "ns1.yp-dns.yandex.net",
            "Nameservers": [
                "ns1.yp-dns.yandex.net",
                "ns2.yp-dns.yandex.net"
            ],
            "YPClusters": [
                "sas-test",
                "man-pre"
            ]
        }
    }
}
```

Запрос и ответ:

```sh
$ curl -X POST -d @req.json http://dns-api-bridge.yp.yandex.net:8080/zone/create/json -v | jq .
{
  "status": "OK",
  "message": "Zone \"test-zone.yandex.net\" has been successfully created"
}
```

{% endcut %}

## RemoveZone {#remove-zone}

Метод позволяет удалить зону, созданную через `CreateZone`.

### Запрос TReqRemoveZone

{% code '/infra/libs/yp_dns/dynamic_zones/zones_manager_service/api/api.proto' lang='protobuf' lines='[BEGIN TReqRemoveZone]-[END TReqRemoveZone]' %}

### Ответ TRspRemoveZone

{% code '/infra/libs/yp_dns/dynamic_zones/zones_manager_service/api/api.proto' lang='protobuf' lines='[BEGIN TRspRemoveZone]-[END TRspRemoveZone]' %}

### Примеры удаления зоны

{% cut "Удаление динамической зоны" %}

```sh
$ curl -X POST -d '{"zone_id":"test-zone.yandex.net"}' http://dns-api-bridge.yp.yandex.net:8080/zone/remove/json -v | jq .
{
  "status": "OK",
  "message": "Zone \"test-zone.yandex.net\" has been successfully removed"
}
```

{% endcut %}
