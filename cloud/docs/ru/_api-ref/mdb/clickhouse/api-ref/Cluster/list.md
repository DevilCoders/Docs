---
editable: false
---

# Метод list
Получает список ClickHouse-кластеров, принадлежащих указанному каталогу.
 

 
## HTTP-запрос {#https-request}
```
GET https://mdb.api.cloud.yandex.net/managed-clickhouse/v1/clusters
```
 
## Query-параметры {#query_params}
 
Параметр | Описание
--- | ---
folderId | Обязательное поле. Идентификатор каталога для вывода списка кластеров ClickHouse. Чтобы получить идентификатор каталога, используйте запрос [list](/docs/resource-manager/api-ref/Folder/list).  Максимальная длина строки в символах — 50.
pageSize | Максимальное количество результатов на одной странице в ответе. Если количество результатов больше чем [pageSize](/docs/managed-clickhouse/api-ref/Cluster/list#query_params), сервис вернет значение [nextPageToken](/docs/managed-clickhouse/api-ref/Cluster/list#responses), которое можно использовать для получения следующей страницы.  Максимальное значение — 1000.
pageToken | Токен страницы. Установите значение [pageToken](/docs/managed-clickhouse/api-ref/Cluster/list#query_params) равным значению поля [nextPageToken](/docs/managed-clickhouse/api-ref/Cluster/list#responses) предыдущего запроса, чтобы получить следующую страницу результатов.  Максимальная длина строки в символах — 100.
filter | Выражение, позволяющее отфильтровать информацию о ресурсах в ответе, оставив только нужную. В этом выражении должны быть указаны: 1. Имя поля. В настоящее время фильтрацию можно использовать только по полю [Cluster.name](/docs/managed-clickhouse/api-ref/Cluster#representation). 2. Условный оператор. Поддерживаются операторы `=` и `!=` для одиночных значений, `IN` и `NOT IN` для списков значений. 3. Значение. Должно содержать от 1 до 63 символов и соответствовать регулярному выражению `^[a-zA-Z0-9_-]+$`.  Максимальная длина строки в символах — 1000.
 
## Ответ {#responses}
**HTTP Code: 200 - OK**

```json 
{
  "clusters": [
    {
      "id": "string",
      "folderId": "string",
      "createdAt": "string",
      "name": "string",
      "description": "string",
      "labels": "object",
      "environment": "string",
      "monitoring": [
        {
          "name": "string",
          "description": "string",
          "link": "string"
        }
      ],
      "config": {
        "version": "string",
        "clickhouse": {
          "config": {
            "effectiveConfig": {
              "logLevel": "string",
              "mergeTree": {
                "replicatedDeduplicationWindow": "integer",
                "replicatedDeduplicationWindowSeconds": "integer",
                "partsToDelayInsert": "integer",
                "partsToThrowInsert": "integer",
                "maxReplicatedMergesInQueue": "integer",
                "numberOfFreeEntriesInPoolToLowerMaxSizeOfMerge": "integer",
                "maxBytesToMergeAtMinSpaceInPool": "integer"
              },
              "compression": [
                {
                  "method": "string",
                  "minPartSize": "string",
                  "minPartSizeRatio": "number"
                }
              ],
              "dictionaries": [
                {
                  "name": "string",
                  "structure": {
                    "id": {
                      "name": "string"
                    },
                    "key": {
                      "attributes": [
                        {
                          "name": "string",
                          "type": "string",
                          "nullValue": "string",
                          "expression": "string",
                          "hierarchical": true,
                          "injective": true
                        }
                      ]
                    },
                    "rangeMin": {
                      "name": "string",
                      "type": "string",
                      "nullValue": "string",
                      "expression": "string",
                      "hierarchical": true,
                      "injective": true
                    },
                    "rangeMax": {
                      "name": "string",
                      "type": "string",
                      "nullValue": "string",
                      "expression": "string",
                      "hierarchical": true,
                      "injective": true
                    },
                    "attributes": [
                      {
                        "name": "string",
                        "type": "string",
                        "nullValue": "string",
                        "expression": "string",
                        "hierarchical": true,
                        "injective": true
                      }
                    ]
                  },
                  "layout": {
                    "type": "string",
                    "sizeInCells": "string"
                  },

                  // `clusters[].config.clickhouse.config.effectiveConfig.dictionaries[]` включает только одно из полей `httpSource`, `mysqlSource`, `clickhouseSource`, `mongodbSource`, `postgresqlSource`
                  "fixedLifetime": "string",
                  "lifetimeRange": {
                    "min": "string",
                    "max": "string"
                  },
                  // конец списка возможных полей`clusters[].config.clickhouse.config.effectiveConfig.dictionaries[]`

                  "httpSource": {
                    "url": "string",
                    "format": "string"
                  },
                  "mysqlSource": {
                    "db": "string",
                    "table": "string",
                    "port": "string",
                    "user": "string",
                    "password": "string",
                    "replicas": [
                      {
                        "host": "string",
                        "priority": "string",
                        "port": "string",
                        "user": "string",
                        "password": "string"
                      }
                    ],
                    "where": "string",
                    "invalidateQuery": "string"
                  },
                  "clickhouseSource": {
                    "db": "string",
                    "table": "string",
                    "host": "string",
                    "port": "string",
                    "user": "string",
                    "password": "string",
                    "where": "string"
                  },
                  "mongodbSource": {
                    "db": "string",
                    "collection": "string",
                    "host": "string",
                    "port": "string",
                    "user": "string",
                    "password": "string"
                  },
                  "postgresqlSource": {
                    "db": "string",
                    "table": "string",
                    "hosts": [
                      "string"
                    ],
                    "port": "string",
                    "user": "string",
                    "password": "string",
                    "invalidateQuery": "string",
                    "sslMode": "string"
                  }
                }
              ],
              "graphiteRollup": [
                {
                  "name": "string",
                  "patterns": [
                    {
                      "regexp": "string",
                      "function": "string",
                      "retention": [
                        {
                          "age": "string",
                          "precision": "string"
                        }
                      ]
                    }
                  ]
                }
              ],
              "maxConnections": "integer",
              "maxConcurrentQueries": "integer",
              "keepAliveTimeout": "integer",
              "uncompressedCacheSize": "integer",
              "markCacheSize": "integer",
              "maxTableSizeToDrop": "integer",
              "maxPartitionSizeToDrop": "integer",
              "builtinDictionariesReloadInterval": "integer",
              "timezone": "string",
              "geobaseUri": "string"
            },
            "userConfig": {
              "logLevel": "string",
              "mergeTree": {
                "replicatedDeduplicationWindow": "integer",
                "replicatedDeduplicationWindowSeconds": "integer",
                "partsToDelayInsert": "integer",
                "partsToThrowInsert": "integer",
                "maxReplicatedMergesInQueue": "integer",
                "numberOfFreeEntriesInPoolToLowerMaxSizeOfMerge": "integer",
                "maxBytesToMergeAtMinSpaceInPool": "integer"
              },
              "compression": [
                {
                  "method": "string",
                  "minPartSize": "string",
                  "minPartSizeRatio": "number"
                }
              ],
              "dictionaries": [
                {
                  "name": "string",
                  "structure": {
                    "id": {
                      "name": "string"
                    },
                    "key": {
                      "attributes": [
                        {
                          "name": "string",
                          "type": "string",
                          "nullValue": "string",
                          "expression": "string",
                          "hierarchical": true,
                          "injective": true
                        }
                      ]
                    },
                    "rangeMin": {
                      "name": "string",
                      "type": "string",
                      "nullValue": "string",
                      "expression": "string",
                      "hierarchical": true,
                      "injective": true
                    },
                    "rangeMax": {
                      "name": "string",
                      "type": "string",
                      "nullValue": "string",
                      "expression": "string",
                      "hierarchical": true,
                      "injective": true
                    },
                    "attributes": [
                      {
                        "name": "string",
                        "type": "string",
                        "nullValue": "string",
                        "expression": "string",
                        "hierarchical": true,
                        "injective": true
                      }
                    ]
                  },
                  "layout": {
                    "type": "string",
                    "sizeInCells": "string"
                  },

                  // `clusters[].config.clickhouse.config.userConfig.dictionaries[]` включает только одно из полей `httpSource`, `mysqlSource`, `clickhouseSource`, `mongodbSource`, `postgresqlSource`
                  "fixedLifetime": "string",
                  "lifetimeRange": {
                    "min": "string",
                    "max": "string"
                  },
                  // конец списка возможных полей`clusters[].config.clickhouse.config.userConfig.dictionaries[]`

                  "httpSource": {
                    "url": "string",
                    "format": "string"
                  },
                  "mysqlSource": {
                    "db": "string",
                    "table": "string",
                    "port": "string",
                    "user": "string",
                    "password": "string",
                    "replicas": [
                      {
                        "host": "string",
                        "priority": "string",
                        "port": "string",
                        "user": "string",
                        "password": "string"
                      }
                    ],
                    "where": "string",
                    "invalidateQuery": "string"
                  },
                  "clickhouseSource": {
                    "db": "string",
                    "table": "string",
                    "host": "string",
                    "port": "string",
                    "user": "string",
                    "password": "string",
                    "where": "string"
                  },
                  "mongodbSource": {
                    "db": "string",
                    "collection": "string",
                    "host": "string",
                    "port": "string",
                    "user": "string",
                    "password": "string"
                  },
                  "postgresqlSource": {
                    "db": "string",
                    "table": "string",
                    "hosts": [
                      "string"
                    ],
                    "port": "string",
                    "user": "string",
                    "password": "string",
                    "invalidateQuery": "string",
                    "sslMode": "string"
                  }
                }
              ],
              "graphiteRollup": [
                {
                  "name": "string",
                  "patterns": [
                    {
                      "regexp": "string",
                      "function": "string",
                      "retention": [
                        {
                          "age": "string",
                          "precision": "string"
                        }
                      ]
                    }
                  ]
                }
              ],
              "maxConnections": "integer",
              "maxConcurrentQueries": "integer",
              "keepAliveTimeout": "integer",
              "uncompressedCacheSize": "integer",
              "markCacheSize": "integer",
              "maxTableSizeToDrop": "integer",
              "maxPartitionSizeToDrop": "integer",
              "builtinDictionariesReloadInterval": "integer",
              "timezone": "string",
              "geobaseUri": "string"
            },
            "defaultConfig": {
              "logLevel": "string",
              "mergeTree": {
                "replicatedDeduplicationWindow": "integer",
                "replicatedDeduplicationWindowSeconds": "integer",
                "partsToDelayInsert": "integer",
                "partsToThrowInsert": "integer",
                "maxReplicatedMergesInQueue": "integer",
                "numberOfFreeEntriesInPoolToLowerMaxSizeOfMerge": "integer",
                "maxBytesToMergeAtMinSpaceInPool": "integer"
              },
              "compression": [
                {
                  "method": "string",
                  "minPartSize": "string",
                  "minPartSizeRatio": "number"
                }
              ],
              "dictionaries": [
                {
                  "name": "string",
                  "structure": {
                    "id": {
                      "name": "string"
                    },
                    "key": {
                      "attributes": [
                        {
                          "name": "string",
                          "type": "string",
                          "nullValue": "string",
                          "expression": "string",
                          "hierarchical": true,
                          "injective": true
                        }
                      ]
                    },
                    "rangeMin": {
                      "name": "string",
                      "type": "string",
                      "nullValue": "string",
                      "expression": "string",
                      "hierarchical": true,
                      "injective": true
                    },
                    "rangeMax": {
                      "name": "string",
                      "type": "string",
                      "nullValue": "string",
                      "expression": "string",
                      "hierarchical": true,
                      "injective": true
                    },
                    "attributes": [
                      {
                        "name": "string",
                        "type": "string",
                        "nullValue": "string",
                        "expression": "string",
                        "hierarchical": true,
                        "injective": true
                      }
                    ]
                  },
                  "layout": {
                    "type": "string",
                    "sizeInCells": "string"
                  },

                  // `clusters[].config.clickhouse.config.defaultConfig.dictionaries[]` включает только одно из полей `httpSource`, `mysqlSource`, `clickhouseSource`, `mongodbSource`, `postgresqlSource`
                  "fixedLifetime": "string",
                  "lifetimeRange": {
                    "min": "string",
                    "max": "string"
                  },
                  // конец списка возможных полей`clusters[].config.clickhouse.config.defaultConfig.dictionaries[]`

                  "httpSource": {
                    "url": "string",
                    "format": "string"
                  },
                  "mysqlSource": {
                    "db": "string",
                    "table": "string",
                    "port": "string",
                    "user": "string",
                    "password": "string",
                    "replicas": [
                      {
                        "host": "string",
                        "priority": "string",
                        "port": "string",
                        "user": "string",
                        "password": "string"
                      }
                    ],
                    "where": "string",
                    "invalidateQuery": "string"
                  },
                  "clickhouseSource": {
                    "db": "string",
                    "table": "string",
                    "host": "string",
                    "port": "string",
                    "user": "string",
                    "password": "string",
                    "where": "string"
                  },
                  "mongodbSource": {
                    "db": "string",
                    "collection": "string",
                    "host": "string",
                    "port": "string",
                    "user": "string",
                    "password": "string"
                  },
                  "postgresqlSource": {
                    "db": "string",
                    "table": "string",
                    "hosts": [
                      "string"
                    ],
                    "port": "string",
                    "user": "string",
                    "password": "string",
                    "invalidateQuery": "string",
                    "sslMode": "string"
                  }
                }
              ],
              "graphiteRollup": [
                {
                  "name": "string",
                  "patterns": [
                    {
                      "regexp": "string",
                      "function": "string",
                      "retention": [
                        {
                          "age": "string",
                          "precision": "string"
                        }
                      ]
                    }
                  ]
                }
              ],
              "maxConnections": "integer",
              "maxConcurrentQueries": "integer",
              "keepAliveTimeout": "integer",
              "uncompressedCacheSize": "integer",
              "markCacheSize": "integer",
              "maxTableSizeToDrop": "integer",
              "maxPartitionSizeToDrop": "integer",
              "builtinDictionariesReloadInterval": "integer",
              "timezone": "string",
              "geobaseUri": "string"
            }
          },
          "resources": {
            "resourcePresetId": "string",
            "diskSize": "string",
            "diskTypeId": "string"
          }
        },
        "zookeeper": {
          "resources": {
            "resourcePresetId": "string",
            "diskSize": "string",
            "diskTypeId": "string"
          }
        },
        "backupWindowStart": {
          "hours": "integer",
          "minutes": "integer",
          "seconds": "integer",
          "nanos": "integer"
        },
        "access": {
          "dataLens": true,
          "webSql": true,
          "metrika": true,
          "serverless": true
        }
      },
      "networkId": "string",
      "health": "string",
      "status": "string",
      "serviceAccountId": "string"
    }
  ],
  "nextPageToken": "string"
}
```

 
Поле | Описание
--- | ---
clusters[] | **object**<br><p>Ресурс Cluster для ClickHouse. Подробнее см. раздел <a href="/docs/managed-clickhouse/concepts">Cluster</a> в руководстве разработчика.</p> 
clusters[].<br>id | **string**<br><p>Идентификатор кластера ClickHouse. Этот идентификатор генерирует MDB при создании кластера.</p> 
clusters[].<br>folderId | **string**<br><p>Идентификатор каталога, которому принадлежит кластер ClickHouse.</p> 
clusters[].<br>createdAt | **string** (date-time)<br><p>Время создания в формате <a href="https://www.ietf.org/rfc/rfc3339.txt">RFC3339</a> .</p> <p>Строка в формате <a href="https://www.ietf.org/rfc/rfc3339.txt">RFC3339</a>.</p> 
clusters[].<br>name | **string**<br><p>Имя кластера ClickHouse. Имя уникально в рамках каталога. Длина 1-63 символов.</p> 
clusters[].<br>description | **string**<br><p>Описание кластера ClickHouse. Длина описания должна быть от 0 до 256 символов.</p> 
clusters[].<br>labels | **object**<br><p>Пользовательские метки для кластера ClickHouse в виде пар ``key:value``. Максимум 64 на ресурс.</p> 
clusters[].<br>environment | **string**<br><p>Среда развертывания кластера ClickHouse.</p> <p>Среда развертывания.</p> <ul> <li>PRODUCTION: Стабильная среда с осторожной политикой обновления: во время регулярного обслуживания применяются только срочные исправления.</li> <li>PRESTABLE: Среда с более агрессивной политикой обновления: новые версии развертываются независимо от обратной совместимости.</li> </ul> 
clusters[].<br>monitoring[] | **object**<br><p>Метаданные системы мониторинга.</p> 
clusters[].<br>monitoring[].<br>name | **string**<br><p>Название системы мониторинга.</p> 
clusters[].<br>monitoring[].<br>description | **string**<br><p>Описание системы мониторинга.</p> 
clusters[].<br>monitoring[].<br>link | **string**<br><p>Ссылка на графики системы мониторинга для данного кластера ClickHouse.</p> 
clusters[].<br>config | **object**<br><p>Конфигурация кластера ClickHouse.</p> 
clusters[].<br>config.<br>version | **string**<br><p>Версия серверного программного обеспечения ClickHouse.</p> 
clusters[].<br>config.<br>clickhouse | **object**<br><p>Конфигурация и распределение ресурсов для хостов ClickHouse.</p> 
clusters[].<br>config.<br>clickhouse.<br>config | **object**<br><p>Параметры конфигурации сервера ClickHouse.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig | **object**<br><p>Обязательное поле. Действующие параметры для кластера ClickHouse (сочетание параметров, определенных в &quot;``userConfig``&quot; и ``defaultConfig``).</p> <p>Настройки конфигурации ClickHouse. Подробное описание для каждого набора настроек доступно в <a href="https://clickhouse.yandex/docs/ru/operations/server_settings/settings/">документации ClickHouse</a>.</p> <p>Любые настройки, не перечисленные здесь, не поддерживаются.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>logLevel | **string**<br><p>Уровень логирования для кластера ClickHouse. Допустимые значения: &quot;TRACE&quot;, &quot;DEBUG&quot;, &quot;INFORMATION&quot;, &quot;WARNING&quot;, &quot;ERROR&quot;. См. описание в <a href="https://clickhouse.yandex/docs/ru/operations/server_settings/settings/#server_settings-logger">документации ClickHouse</a>.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>mergeTree | **object**<br><p>Параметры движка MergeTree. См. описание в <a href="https://clickhouse.yandex/docs/ru/operations/server_settings/settings/#merge_tree">документации ClickHouse</a>.</p> <p>Настройки движка таблицы MergeTree.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>mergeTree.<br>replicatedDeduplicationWindow | **integer** (int64)<br><p>Количество блоков хэшей, которые должен хранить ZooKeeper. Смотрите подробное описание в <a href="https://github.com/yandex/ClickHouse/blob/v18.1.0-stable/dbms/src/Storages/MergeTree/MergeTreeSettings.h#L59">ClickHouse sources</a>.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>mergeTree.<br>replicatedDeduplicationWindowSeconds | **integer** (int64)<br><p>Период времени, в течение которого следует хранить блоки хэшей. См. описание в <a href="https://github.com/yandex/ClickHouse/blob/v18.1.0-stable/dbms/src/Storages/MergeTree/MergeTreeSettings.h#L64">ClickHouse sources</a>.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>mergeTree.<br>partsToDelayInsert | **integer** (int64)<br>
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>mergeTree.<br>partsToThrowInsert | **integer** (int64)<br>
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>mergeTree.<br>maxReplicatedMergesInQueue | **integer** (int64)<br>
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>mergeTree.<br>numberOfFreeEntriesInPoolToLowerMaxSizeOfMerge | **integer** (int64)<br>
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>mergeTree.<br>maxBytesToMergeAtMinSpaceInPool | **integer** (int64)<br>
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>compression[] | **object**<br><p>Параметры сжатия для кластера ClickHouse. См. подробное описание в <a href="https://clickhouse.yandex/docs/ru/operations/server_settings/settings/#compression">документации ClickHouse</a>.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>compression[].<br>method | **string**<br><p>Метод сжатия, используемый для указанной комбинации &quot;min_part_size&quot; и &quot;min_part_size_ratio&quot;.</p> <ul> <li>LZ4: <a href="https://lz4.github.io/lz4/">LZ4 compression algorithm</a>.</li> <li>ZSTD: <a href="https://facebook.github.io/zstd/">Zstandard compression algorithm</a>.</li> </ul> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>compression[].<br>minPartSize | **string** (int64)<br><p>Минимальный размер части таблицы.</p> <p>Минимальное значение — 1.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>compression[].<br>minPartSizeRatio | **number** (double)<br><p>Минимальное отношение части к размеру всех данных в таблице.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[] | **object**<br><p>Конфигурация внешних словарей для кластера ClickHouse. См. подробное описание в <a href="https://clickhouse.yandex/docs/ru/query_language/dicts/external_dicts/">документации ClickHouse</a>.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>name | **string**<br><p>Обязательное поле. Имя внешнего словаря.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>structure | **object**<br>Обязательное поле. Набор атрибутов внешнего словаря. Подробное описание см. в [документации ClickHouse](https://clickhouse.yandex/docs/ru/query_language/dicts/external_dicts_dict_structure/).<br>
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>structure.<br>id | **object**<br><p>Один столбец с числовыми ключами для словаря.</p> <p>Числовой ключ.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>structure.<br>id.<br>name | **string**<br><p>Обязательное поле. Имя числового ключа.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>structure.<br>key | **object**<br><p>Составной ключ для словаря, содержащего один или несколько столбцов с ключами. Подробнее см. в <a href="https://clickhouse.yandex/docs/ru/query_language/dicts/external_dicts_dict_structure/#composite-key">документации ClickHouse</a>.</p> <p>Составной ключ.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>structure.<br>key.<br>attributes[] | **object**<br><p>Обязательное поле. Поля составного ключа.</p> <p>Должен содержать хотя бы один элемент.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>structure.<br>key.<br>attributes[].<br>name | **string**<br><p>Обязательное поле. Имя столбца.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>structure.<br>key.<br>attributes[].<br>type | **string**<br><p>Обязательное поле. Тип столбца.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>structure.<br>key.<br>attributes[].<br>nullValue | **string**<br><p>Значение по умолчанию для элемента без данных (например, пустая строка).</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>structure.<br>key.<br>attributes[].<br>expression | **string**<br><p>Выражение, описывающее атрибут, если применимо.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>structure.<br>key.<br>attributes[].<br>hierarchical | **boolean** (boolean)<br><p>Признак поддержки иерархии. Значение по умолчанию &quot;false&quot;.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>structure.<br>key.<br>attributes[].<br>injective | **boolean** (boolean)<br><p>Признакт инъективного отображения &quot;id -&gt; атрибут&quot;. Значение по умолчанию &quot;false&quot;.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>structure.<br>rangeMin | **object**<br><p>Поле, содержащее начало диапазона для словарей, которые хранятся в памяти способом &quot;RANGE_HASHED&quot;. Подробнее см.<a href="https://clickhouse.yandex/docs/ru/query_language/dicts/external_dicts_dict_layout/#range-hashed">документации ClickHouse</a></p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>structure.<br>rangeMin.<br>name | **string**<br><p>Обязательное поле. Имя столбца.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>structure.<br>rangeMin.<br>type | **string**<br><p>Обязательное поле. Тип столбца.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>structure.<br>rangeMin.<br>nullValue | **string**<br><p>Значение по умолчанию для элемента без данных (например, пустая строка).</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>structure.<br>rangeMin.<br>expression | **string**<br><p>Выражение, описывающее атрибут, если применимо.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>structure.<br>rangeMin.<br>hierarchical | **boolean** (boolean)<br><p>Признак поддержки иерархии. Значение по умолчанию &quot;false&quot;.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>structure.<br>rangeMin.<br>injective | **boolean** (boolean)<br><p>Признакт инъективного отображения &quot;id -&gt; атрибут&quot;. Значение по умолчанию &quot;false&quot;.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>structure.<br>rangeMax | **object**<br><p>Поле, содержащее конец диапазона для словарей, которые хранятся в памяти способом &quot;RANGE_HASHED&quot;. Подробнее см.<a href="https://clickhouse.yandex/docs/ru/query_language/dicts/external_dicts_dict_layout/#range-hashed">документации ClickHouse</a></p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>structure.<br>rangeMax.<br>name | **string**<br><p>Обязательное поле. Имя столбца.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>structure.<br>rangeMax.<br>type | **string**<br><p>Обязательное поле. Тип столбца.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>structure.<br>rangeMax.<br>nullValue | **string**<br><p>Значение по умолчанию для элемента без данных (например, пустая строка).</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>structure.<br>rangeMax.<br>expression | **string**<br><p>Выражение, описывающее атрибут, если применимо.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>structure.<br>rangeMax.<br>hierarchical | **boolean** (boolean)<br><p>Признак поддержки иерархии. Значение по умолчанию &quot;false&quot;.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>structure.<br>rangeMax.<br>injective | **boolean** (boolean)<br><p>Признакт инъективного отображения &quot;id -&gt; атрибут&quot;. Значение по умолчанию &quot;false&quot;.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>structure.<br>attributes[] | **object**<br><p>Обязательное поле. Описание полей, доступных для запросов к базе данных. Подробнее см. в <a href="https://clickhouse.yandex/docs/ru/query_language/dicts/external_dicts_dict_structure/#attributes">документации ClickHouse</a>.</p> <p>Должен содержать хотя бы один элемент.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>structure.<br>attributes[].<br>name | **string**<br><p>Обязательное поле. Имя столбца.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>structure.<br>attributes[].<br>type | **string**<br><p>Обязательное поле. Тип столбца.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>structure.<br>attributes[].<br>nullValue | **string**<br><p>Значение по умолчанию для элемента без данных (например, пустая строка).</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>structure.<br>attributes[].<br>expression | **string**<br><p>Выражение, описывающее атрибут, если применимо.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>structure.<br>attributes[].<br>hierarchical | **boolean** (boolean)<br><p>Признак поддержки иерархии. Значение по умолчанию &quot;false&quot;.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>structure.<br>attributes[].<br>injective | **boolean** (boolean)<br><p>Признакт инъективного отображения &quot;id -&gt; атрибут&quot;. Значение по умолчанию &quot;false&quot;.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>layout | **object**<br>Обязательное поле. Макет для хранения словаря в памяти. Подробное описание см. в [документации ClickHouse](https://clickhouse.yandex/docs/ru/query_language/dicts/external_dicts_dict_layout/).<br><p>Макет, определяющий способ хранения словаря в памяти.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>layout.<br>type | **string**<br><p>Обязательное поле. Тип макета для внешнего словаря.</p> <ul> <li>FLAT: Весь словарь хранится в памяти в виде плоских массивов. Доступно для любых источников словарей.</li> <li>HASHED: Весь словарь хранится в памяти в виде хэш-таблицы. Доступно для любых источников словарей.</li> <li>COMPLEX_KEY_HASHED: Аналогичен HASHED, для использования с составными ключами. Доступно для любых источников словарей.</li> <li>RANGE_HASHED: Весь словарь хранится в памяти в виде хэш-таблицы, с упорядоченным массивом диапазонов и соответствующих им значений. Доступно для любых источников словарей.</li> <li>CACHE: Словарь хранится в кэше с заданным количеством ячеек. Доступно для источников словарей MySQL, ClickHouse и HTTP.</li> <li>COMPLEX_KEY_CACHE: Аналогичен CACHE, для использования с составными ключами. Доступно для источников словарей MySQL, ClickHouse и HTTP.</li> </ul> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>layout.<br>sizeInCells | **string** (int64)<br><p>Количество ячеек в кэше. Округляется до степени двойки. Применимо только для типов макета CACHE и COMPLEX_KEY_CACHE.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>fixedLifetime | **string** (int64) <br>`clusters[].config.clickhouse.config.effectiveConfig.dictionaries[]` включает только одно из полей `fixedLifetime`, `lifetimeRange`<br><br><p>Жесткий интервал между обновлениями словаря.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>lifetimeRange | **object**<br>Диапазон интервалов между обновлениями словаря, из которых может выбирать ClickHouse. <br>`clusters[].config.clickhouse.config.effectiveConfig.dictionaries[]` включает только одно из полей `fixedLifetime`, `lifetimeRange`<br><br>
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>lifetimeRange.<br>min | **string** (int64)<br><p>Минимальное время жизни словаря.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>lifetimeRange.<br>max | **string** (int64)<br><p>Максимальное время жизни словаря.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>httpSource | **object**<br>HTTP-источник для словаря. <br>`clusters[].config.clickhouse.config.effectiveConfig.dictionaries[]` включает только одно из полей `httpSource`, `mysqlSource`, `clickhouseSource`, `mongodbSource`, `postgresqlSource`<br><br>
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>httpSource.<br>url | **string**<br><p>Обязательное поле. URL внешнего словаря, доступного по HTTP.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>httpSource.<br>format | **string**<br><p>Обязательное поле. Формат данных. Допустимые значения: все форматы, поддерживаемые диалектом ClickHouse SQL.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>mysqlSource | **object**<br>MySQL-источник для словаря. <br>`clusters[].config.clickhouse.config.effectiveConfig.dictionaries[]` включает только одно из полей `httpSource`, `mysqlSource`, `clickhouseSource`, `mongodbSource`, `postgresqlSource`<br><br>
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>mysqlSource.<br>db | **string**<br><p>Обязательное поле. Имя базы данных MySQL, к которой нужно подключаться.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>mysqlSource.<br>table | **string**<br><p>Обязательное поле. Имя таблицы базы данных, которую следует использовать в качестве словаря ClickHouse.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>mysqlSource.<br>port | **string** (int64)<br><p>Порт по умолчанию, который нужно использовать при подключении к реплике источника словаря.</p> <p>Допустимые значения — от 0 до 65535 включительно.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>mysqlSource.<br>user | **string**<br><p>Имя пользователя по умолчанию для реплик источника словаря.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>mysqlSource.<br>password | **string**<br><p>Пароль пользователя по умолчанию для реплик источника словаря.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>mysqlSource.<br>replicas[] | **object**<br><p>Обязательное поле. Список реплик базы данных MySQL, используемой в качестве источника словаря.</p> <p>Должен содержать хотя бы один элемент.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>mysqlSource.<br>replicas[].<br>host | **string**<br><p>Обязательное поле. Хост реплики MySQL.</p> <p>Максимальная длина строки в символах — 253.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>mysqlSource.<br>replicas[].<br>priority | **string** (int64)<br><p>Обязательное поле. Приоритет реплики, который ClickHouse должен учитывать при подключении. Реплике с наивысшим приоритетом должно соответствовать наименьшее значение в этом поле.</p> <p>Значение должно быть больше 0.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>mysqlSource.<br>replicas[].<br>port | **string** (int64)<br><p>Порт, который нужно использовать при подключении к реплике. Если для какой-либо реплики не указан порт, ClickHouse использует порт, указанный для источника.</p> <p>Допустимые значения — от 0 до 65535 включительно.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>mysqlSource.<br>replicas[].<br>user | **string**<br><p>Имя пользователя базы данных MySQL.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>mysqlSource.<br>replicas[].<br>password | **string**<br><p>Пароль пользователя базы данных MySQL.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>mysqlSource.<br>where | **string**<br><p>Критерии выбора данных в указанной таблице MySQL.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>mysqlSource.<br>invalidateQuery | **string**<br><p>Запрос на проверку состояния словаря, который позволит извлекать только обновленные данные. Дополнительные сведения см. в <a href="https://clickhouse.yandex/docs/ru/query_language/dicts/external_dicts_dict_lifetime/">документации ClickHouse on dictionaries</a>.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>clickhouseSource | **object**<br>ClickHouse-источник для словаря. <br>`clusters[].config.clickhouse.config.effectiveConfig.dictionaries[]` включает только одно из полей `httpSource`, `mysqlSource`, `clickhouseSource`, `mongodbSource`, `postgresqlSource`<br><br>
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>clickhouseSource.<br>db | **string**<br><p>Обязательное поле. Имя базы данных ClickHouse.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>clickhouseSource.<br>table | **string**<br><p>Обязательное поле. Имя таблицы в указанной базе данных, используемой в качестве источника словаря.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>clickhouseSource.<br>host | **string**<br><p>Обязательное поле. Хост ClickHouse для указанной базы данных.</p> <p>Максимальная длина строки в символах — 253.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>clickhouseSource.<br>port | **string** (int64)<br><p>Порт для подключения к хосту.</p> <p>Допустимые значения — от 0 до 65535 включительно.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>clickhouseSource.<br>user | **string**<br><p>Обязательное поле. Имя пользователя базы данных ClickHouse.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>clickhouseSource.<br>password | **string**<br><p>Пароль пользователя базы данных ClickHouse.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>clickhouseSource.<br>where | **string**<br><p>Критерии выбора данных в указанной таблице ClickHouse.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>mongodbSource | **object**<br>MongoDB-источник для словаря. <br>`clusters[].config.clickhouse.config.effectiveConfig.dictionaries[]` включает только одно из полей `httpSource`, `mysqlSource`, `clickhouseSource`, `mongodbSource`, `postgresqlSource`<br><br>
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>mongodbSource.<br>db | **string**<br><p>Обязательное поле. Имя базы данных MongoDB.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>mongodbSource.<br>collection | **string**<br><p>Обязательное поле. Имя коллекции в указанной базе данных, которую следует использовать в качестве источника словаря.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>mongodbSource.<br>host | **string**<br><p>Обязательное поле. Хост MongoDB для указанной базы данных.</p> <p>Максимальная длина строки в символах — 253.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>mongodbSource.<br>port | **string** (int64)<br><p>Порт для подключения к хосту.</p> <p>Допустимые значения — от 0 до 65535 включительно.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>mongodbSource.<br>user | **string**<br><p>Обязательное поле. Имя пользователя базы данных MongoDB.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>mongodbSource.<br>password | **string**<br><p>Пароль пользователя базы данных MongoDB.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>postgresqlSource | **object**<br>PostgreSQL-источник для словаря. <br>`clusters[].config.clickhouse.config.effectiveConfig.dictionaries[]` включает только одно из полей `httpSource`, `mysqlSource`, `clickhouseSource`, `mongodbSource`, `postgresqlSource`<br><br>
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>postgresqlSource.<br>db | **string**<br><p>Обязательное поле. Имя базы данных PostrgreSQL.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>postgresqlSource.<br>table | **string**<br><p>Обязательное поле. Имя таблицы в указанной базе данных, используемой в качестве источника словаря.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>postgresqlSource.<br>hosts[] | **string**<br><p>Обязательное поле. Имя хоста PostrgreSQL.</p> <p>Должен содержать хотя бы один элемент.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>postgresqlSource.<br>port | **string** (int64)<br><p>Порт для подключения к хосту.</p> <p>Допустимые значения — от 0 до 65535 включительно.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>postgresqlSource.<br>user | **string**<br><p>Обязательное поле. Имя пользователя базы данных PostrgreSQL.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>postgresqlSource.<br>password | **string**<br><p>Пароль пользователя базы данных PostrgreSQL.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>postgresqlSource.<br>invalidateQuery | **string**<br><p>Запрос на проверку состояния словаря, который позволит извлекать только обновленные данные. Дополнительные сведения см. в <a href="https://clickhouse.yandex/docs/ru/query_language/dicts/external_dicts_dict_lifetime/">документации ClickHouse on dictionaries</a>.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>dictionaries[].<br>postgresqlSource.<br>sslMode | **string**<br><p>Режим SSL TCP/IP соединения с хостом PostgreSQL. Дополнительные сведения см. в <a href="https://www.postgresql.org/docs/current/libpq-ssl.html">PostgreSQL documentation</a>.</p> <ul> <li>DISABLE: SSL-соединение не используется.</li> <li>ALLOW: Сначала предпринимается попытка установить незашифрованное соединение. Если это не удается, устанавливается SSL-соединение.</li> <li>PREFER: Сначала предпринимается попытка установить SSL-соединение. Если это не удается, устанавливается незашифрованное соединение.</li> <li>VERIFY_CA: Устанавливается только SSL-соединение и только при условии, что сертификат выдан доверенным центром сертификации (CA).</li> <li>VERIFY_FULL: Устанавливается только SSL-соединение и только при условии, что сертификат выдан доверенным центром сертификации и что имя хоста сервера совпадает с указанным в сертификате.</li> </ul> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>graphiteRollup[] | **object**<br><p>Параметры свертки для движка таблицы GraphiteMergeTree.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>graphiteRollup[].<br>name | **string**<br><p>Обязательное поле. Имя указанной комбинации параметров для свертки Graphite.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>graphiteRollup[].<br>patterns[] | **object**<br><p>Обязательное поле. Шаблон, используемый для свертки.</p> <p>Должен содержать хотя бы один элемент.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>graphiteRollup[].<br>patterns[].<br>regexp | **string**<br><p>Шаблон для имен метрик.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>graphiteRollup[].<br>patterns[].<br>function | **string**<br><p>Обязательное поле. Имя агрегирующей функции, которую следует применить к данным старше возраста, указанного в &quot;``retention``&quot;.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>graphiteRollup[].<br>patterns[].<br>retention[] | **object**<br><p>Обязательное поле. Возраст данных, которые следует использовать для прореживания.</p> <p>Должен содержать хотя бы один элемент.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>graphiteRollup[].<br>patterns[].<br>retention[].<br>age | **string** (int64)<br><p>Минимальный возраст данных в секундах.</p> <p>Значение должно быть больше 0.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>graphiteRollup[].<br>patterns[].<br>retention[].<br>precision | **string** (int64)<br><p>Точность определения возраста данных, в секундах.</p> <p>Значение должно быть больше 0.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>maxConnections | **integer** (int64)<br><p>Максимальное количество входящих подключений.</p> <p>Минимальное значение — 10.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>maxConcurrentQueries | **integer** (int64)<br><p>Максимальное количество одновременно обрабатываемых запросов.</p> <p>Минимальное значение — 10.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>keepAliveTimeout | **integer** (int64)<br><p>Количество миллисекунд, в течение которых ClickHouse ожидает входящие запросы прежде чем закрыть подключение.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>uncompressedCacheSize | **integer** (int64)<br><p>Размер кэша (в байтах) для несжатых данных, используемых таблицами MergeTree. См. подробное описание в <a href="https://clickhouse.yandex/docs/ru/operations/server_settings/settings/#uncompressed_cache_size">документации ClickHouse</a>.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>markCacheSize | **integer** (int64)<br><p>Примерный размер (в байтах) кэша «меток», используемых таблицами MergeTree. Подробнее в <a href="https://clickhouse.yandex/docs/ru/operations/server_settings/settings/#mark_cache_size">документации ClickHouse</a>.</p> <p>Значение должно быть больше 5368709120.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>maxTableSizeToDrop | **integer** (int64)<br><p>Максимальный размер таблицы, которую можно удалить с помощью запроса DROP. См. подробное описание в <a href="https://clickhouse.yandex/docs/ru/operations/server_settings/settings/#max_table_size_to_drop">документации ClickHouse</a>.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>maxPartitionSizeToDrop | **integer** (int64)<br><p>Максимальный размер раздела, который можно удалить с помощью запроса DROP. См. подробное описание в <a href="https://clickhouse.yandex/docs/ru/operations/server_settings/settings/#max_partition_size_to_drop">документации ClickHouse</a>.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>builtinDictionariesReloadInterval | **integer** (int64)<br><p>Параметр устарел и не имеет никакого эффекта.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>timezone | **string**<br><p>Часовой пояс сервера, используемый в преобразованиях полей DateTime. Указывается как идентификатор IANA. См. подробное описание в <a href="https://clickhouse.yandex/docs/ru/operations/server_settings/settings/#timezone">документации ClickHouse</a>.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>effectiveConfig.<br>geobaseUri | **string**<br>
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig | **object**<br><p>Пользовательские настройки для кластера ClickHouse.</p> <p>Настройки конфигурации ClickHouse. Подробное описание для каждого набора настроек доступно в <a href="https://clickhouse.yandex/docs/ru/operations/server_settings/settings/">документации ClickHouse</a>.</p> <p>Любые настройки, не перечисленные здесь, не поддерживаются.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>logLevel | **string**<br><p>Уровень логирования для кластера ClickHouse. Допустимые значения: &quot;TRACE&quot;, &quot;DEBUG&quot;, &quot;INFORMATION&quot;, &quot;WARNING&quot;, &quot;ERROR&quot;. См. описание в <a href="https://clickhouse.yandex/docs/ru/operations/server_settings/settings/#server_settings-logger">документации ClickHouse</a>.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>mergeTree | **object**<br><p>Параметры движка MergeTree. См. описание в <a href="https://clickhouse.yandex/docs/ru/operations/server_settings/settings/#merge_tree">документации ClickHouse</a>.</p> <p>Настройки движка таблицы MergeTree.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>mergeTree.<br>replicatedDeduplicationWindow | **integer** (int64)<br><p>Количество блоков хэшей, которые должен хранить ZooKeeper. Смотрите подробное описание в <a href="https://github.com/yandex/ClickHouse/blob/v18.1.0-stable/dbms/src/Storages/MergeTree/MergeTreeSettings.h#L59">ClickHouse sources</a>.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>mergeTree.<br>replicatedDeduplicationWindowSeconds | **integer** (int64)<br><p>Период времени, в течение которого следует хранить блоки хэшей. См. описание в <a href="https://github.com/yandex/ClickHouse/blob/v18.1.0-stable/dbms/src/Storages/MergeTree/MergeTreeSettings.h#L64">ClickHouse sources</a>.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>mergeTree.<br>partsToDelayInsert | **integer** (int64)<br>
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>mergeTree.<br>partsToThrowInsert | **integer** (int64)<br>
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>mergeTree.<br>maxReplicatedMergesInQueue | **integer** (int64)<br>
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>mergeTree.<br>numberOfFreeEntriesInPoolToLowerMaxSizeOfMerge | **integer** (int64)<br>
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>mergeTree.<br>maxBytesToMergeAtMinSpaceInPool | **integer** (int64)<br>
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>compression[] | **object**<br><p>Параметры сжатия для кластера ClickHouse. См. подробное описание в <a href="https://clickhouse.yandex/docs/ru/operations/server_settings/settings/#compression">документации ClickHouse</a>.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>compression[].<br>method | **string**<br><p>Метод сжатия, используемый для указанной комбинации &quot;min_part_size&quot; и &quot;min_part_size_ratio&quot;.</p> <ul> <li>LZ4: <a href="https://lz4.github.io/lz4/">LZ4 compression algorithm</a>.</li> <li>ZSTD: <a href="https://facebook.github.io/zstd/">Zstandard compression algorithm</a>.</li> </ul> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>compression[].<br>minPartSize | **string** (int64)<br><p>Минимальный размер части таблицы.</p> <p>Минимальное значение — 1.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>compression[].<br>minPartSizeRatio | **number** (double)<br><p>Минимальное отношение части к размеру всех данных в таблице.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[] | **object**<br><p>Конфигурация внешних словарей для кластера ClickHouse. См. подробное описание в <a href="https://clickhouse.yandex/docs/ru/query_language/dicts/external_dicts/">документации ClickHouse</a>.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>name | **string**<br><p>Обязательное поле. Имя внешнего словаря.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>structure | **object**<br>Обязательное поле. Набор атрибутов внешнего словаря. Подробное описание см. в [документации ClickHouse](https://clickhouse.yandex/docs/ru/query_language/dicts/external_dicts_dict_structure/).<br>
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>structure.<br>id | **object**<br><p>Один столбец с числовыми ключами для словаря.</p> <p>Числовой ключ.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>structure.<br>id.<br>name | **string**<br><p>Обязательное поле. Имя числового ключа.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>structure.<br>key | **object**<br><p>Составной ключ для словаря, содержащего один или несколько столбцов с ключами. Подробнее см. в <a href="https://clickhouse.yandex/docs/ru/query_language/dicts/external_dicts_dict_structure/#composite-key">документации ClickHouse</a>.</p> <p>Составной ключ.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>structure.<br>key.<br>attributes[] | **object**<br><p>Обязательное поле. Поля составного ключа.</p> <p>Должен содержать хотя бы один элемент.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>structure.<br>key.<br>attributes[].<br>name | **string**<br><p>Обязательное поле. Имя столбца.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>structure.<br>key.<br>attributes[].<br>type | **string**<br><p>Обязательное поле. Тип столбца.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>structure.<br>key.<br>attributes[].<br>nullValue | **string**<br><p>Значение по умолчанию для элемента без данных (например, пустая строка).</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>structure.<br>key.<br>attributes[].<br>expression | **string**<br><p>Выражение, описывающее атрибут, если применимо.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>structure.<br>key.<br>attributes[].<br>hierarchical | **boolean** (boolean)<br><p>Признак поддержки иерархии. Значение по умолчанию &quot;false&quot;.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>structure.<br>key.<br>attributes[].<br>injective | **boolean** (boolean)<br><p>Признакт инъективного отображения &quot;id -&gt; атрибут&quot;. Значение по умолчанию &quot;false&quot;.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>structure.<br>rangeMin | **object**<br><p>Поле, содержащее начало диапазона для словарей, которые хранятся в памяти способом &quot;RANGE_HASHED&quot;. Подробнее см.<a href="https://clickhouse.yandex/docs/ru/query_language/dicts/external_dicts_dict_layout/#range-hashed">документации ClickHouse</a></p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>structure.<br>rangeMin.<br>name | **string**<br><p>Обязательное поле. Имя столбца.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>structure.<br>rangeMin.<br>type | **string**<br><p>Обязательное поле. Тип столбца.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>structure.<br>rangeMin.<br>nullValue | **string**<br><p>Значение по умолчанию для элемента без данных (например, пустая строка).</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>structure.<br>rangeMin.<br>expression | **string**<br><p>Выражение, описывающее атрибут, если применимо.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>structure.<br>rangeMin.<br>hierarchical | **boolean** (boolean)<br><p>Признак поддержки иерархии. Значение по умолчанию &quot;false&quot;.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>structure.<br>rangeMin.<br>injective | **boolean** (boolean)<br><p>Признакт инъективного отображения &quot;id -&gt; атрибут&quot;. Значение по умолчанию &quot;false&quot;.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>structure.<br>rangeMax | **object**<br><p>Поле, содержащее конец диапазона для словарей, которые хранятся в памяти способом &quot;RANGE_HASHED&quot;. Подробнее см.<a href="https://clickhouse.yandex/docs/ru/query_language/dicts/external_dicts_dict_layout/#range-hashed">документации ClickHouse</a></p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>structure.<br>rangeMax.<br>name | **string**<br><p>Обязательное поле. Имя столбца.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>structure.<br>rangeMax.<br>type | **string**<br><p>Обязательное поле. Тип столбца.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>structure.<br>rangeMax.<br>nullValue | **string**<br><p>Значение по умолчанию для элемента без данных (например, пустая строка).</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>structure.<br>rangeMax.<br>expression | **string**<br><p>Выражение, описывающее атрибут, если применимо.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>structure.<br>rangeMax.<br>hierarchical | **boolean** (boolean)<br><p>Признак поддержки иерархии. Значение по умолчанию &quot;false&quot;.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>structure.<br>rangeMax.<br>injective | **boolean** (boolean)<br><p>Признакт инъективного отображения &quot;id -&gt; атрибут&quot;. Значение по умолчанию &quot;false&quot;.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>structure.<br>attributes[] | **object**<br><p>Обязательное поле. Описание полей, доступных для запросов к базе данных. Подробнее см. в <a href="https://clickhouse.yandex/docs/ru/query_language/dicts/external_dicts_dict_structure/#attributes">документации ClickHouse</a>.</p> <p>Должен содержать хотя бы один элемент.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>structure.<br>attributes[].<br>name | **string**<br><p>Обязательное поле. Имя столбца.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>structure.<br>attributes[].<br>type | **string**<br><p>Обязательное поле. Тип столбца.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>structure.<br>attributes[].<br>nullValue | **string**<br><p>Значение по умолчанию для элемента без данных (например, пустая строка).</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>structure.<br>attributes[].<br>expression | **string**<br><p>Выражение, описывающее атрибут, если применимо.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>structure.<br>attributes[].<br>hierarchical | **boolean** (boolean)<br><p>Признак поддержки иерархии. Значение по умолчанию &quot;false&quot;.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>structure.<br>attributes[].<br>injective | **boolean** (boolean)<br><p>Признакт инъективного отображения &quot;id -&gt; атрибут&quot;. Значение по умолчанию &quot;false&quot;.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>layout | **object**<br>Обязательное поле. Макет для хранения словаря в памяти. Подробное описание см. в [документации ClickHouse](https://clickhouse.yandex/docs/ru/query_language/dicts/external_dicts_dict_layout/).<br><p>Макет, определяющий способ хранения словаря в памяти.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>layout.<br>type | **string**<br><p>Обязательное поле. Тип макета для внешнего словаря.</p> <ul> <li>FLAT: Весь словарь хранится в памяти в виде плоских массивов. Доступно для любых источников словарей.</li> <li>HASHED: Весь словарь хранится в памяти в виде хэш-таблицы. Доступно для любых источников словарей.</li> <li>COMPLEX_KEY_HASHED: Аналогичен HASHED, для использования с составными ключами. Доступно для любых источников словарей.</li> <li>RANGE_HASHED: Весь словарь хранится в памяти в виде хэш-таблицы, с упорядоченным массивом диапазонов и соответствующих им значений. Доступно для любых источников словарей.</li> <li>CACHE: Словарь хранится в кэше с заданным количеством ячеек. Доступно для источников словарей MySQL, ClickHouse и HTTP.</li> <li>COMPLEX_KEY_CACHE: Аналогичен CACHE, для использования с составными ключами. Доступно для источников словарей MySQL, ClickHouse и HTTP.</li> </ul> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>layout.<br>sizeInCells | **string** (int64)<br><p>Количество ячеек в кэше. Округляется до степени двойки. Применимо только для типов макета CACHE и COMPLEX_KEY_CACHE.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>fixedLifetime | **string** (int64) <br>`clusters[].config.clickhouse.config.userConfig.dictionaries[]` включает только одно из полей `fixedLifetime`, `lifetimeRange`<br><br><p>Жесткий интервал между обновлениями словаря.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>lifetimeRange | **object**<br>Диапазон интервалов между обновлениями словаря, из которых может выбирать ClickHouse. <br>`clusters[].config.clickhouse.config.userConfig.dictionaries[]` включает только одно из полей `fixedLifetime`, `lifetimeRange`<br><br>
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>lifetimeRange.<br>min | **string** (int64)<br><p>Минимальное время жизни словаря.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>lifetimeRange.<br>max | **string** (int64)<br><p>Максимальное время жизни словаря.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>httpSource | **object**<br>HTTP-источник для словаря. <br>`clusters[].config.clickhouse.config.userConfig.dictionaries[]` включает только одно из полей `httpSource`, `mysqlSource`, `clickhouseSource`, `mongodbSource`, `postgresqlSource`<br><br>
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>httpSource.<br>url | **string**<br><p>Обязательное поле. URL внешнего словаря, доступного по HTTP.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>httpSource.<br>format | **string**<br><p>Обязательное поле. Формат данных. Допустимые значения: все форматы, поддерживаемые диалектом ClickHouse SQL.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>mysqlSource | **object**<br>MySQL-источник для словаря. <br>`clusters[].config.clickhouse.config.userConfig.dictionaries[]` включает только одно из полей `httpSource`, `mysqlSource`, `clickhouseSource`, `mongodbSource`, `postgresqlSource`<br><br>
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>mysqlSource.<br>db | **string**<br><p>Обязательное поле. Имя базы данных MySQL, к которой нужно подключаться.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>mysqlSource.<br>table | **string**<br><p>Обязательное поле. Имя таблицы базы данных, которую следует использовать в качестве словаря ClickHouse.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>mysqlSource.<br>port | **string** (int64)<br><p>Порт по умолчанию, который нужно использовать при подключении к реплике источника словаря.</p> <p>Допустимые значения — от 0 до 65535 включительно.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>mysqlSource.<br>user | **string**<br><p>Имя пользователя по умолчанию для реплик источника словаря.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>mysqlSource.<br>password | **string**<br><p>Пароль пользователя по умолчанию для реплик источника словаря.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>mysqlSource.<br>replicas[] | **object**<br><p>Обязательное поле. Список реплик базы данных MySQL, используемой в качестве источника словаря.</p> <p>Должен содержать хотя бы один элемент.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>mysqlSource.<br>replicas[].<br>host | **string**<br><p>Обязательное поле. Хост реплики MySQL.</p> <p>Максимальная длина строки в символах — 253.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>mysqlSource.<br>replicas[].<br>priority | **string** (int64)<br><p>Обязательное поле. Приоритет реплики, который ClickHouse должен учитывать при подключении. Реплике с наивысшим приоритетом должно соответствовать наименьшее значение в этом поле.</p> <p>Значение должно быть больше 0.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>mysqlSource.<br>replicas[].<br>port | **string** (int64)<br><p>Порт, который нужно использовать при подключении к реплике. Если для какой-либо реплики не указан порт, ClickHouse использует порт, указанный для источника.</p> <p>Допустимые значения — от 0 до 65535 включительно.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>mysqlSource.<br>replicas[].<br>user | **string**<br><p>Имя пользователя базы данных MySQL.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>mysqlSource.<br>replicas[].<br>password | **string**<br><p>Пароль пользователя базы данных MySQL.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>mysqlSource.<br>where | **string**<br><p>Критерии выбора данных в указанной таблице MySQL.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>mysqlSource.<br>invalidateQuery | **string**<br><p>Запрос на проверку состояния словаря, который позволит извлекать только обновленные данные. Дополнительные сведения см. в <a href="https://clickhouse.yandex/docs/ru/query_language/dicts/external_dicts_dict_lifetime/">документации ClickHouse on dictionaries</a>.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>clickhouseSource | **object**<br>ClickHouse-источник для словаря. <br>`clusters[].config.clickhouse.config.userConfig.dictionaries[]` включает только одно из полей `httpSource`, `mysqlSource`, `clickhouseSource`, `mongodbSource`, `postgresqlSource`<br><br>
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>clickhouseSource.<br>db | **string**<br><p>Обязательное поле. Имя базы данных ClickHouse.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>clickhouseSource.<br>table | **string**<br><p>Обязательное поле. Имя таблицы в указанной базе данных, используемой в качестве источника словаря.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>clickhouseSource.<br>host | **string**<br><p>Обязательное поле. Хост ClickHouse для указанной базы данных.</p> <p>Максимальная длина строки в символах — 253.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>clickhouseSource.<br>port | **string** (int64)<br><p>Порт для подключения к хосту.</p> <p>Допустимые значения — от 0 до 65535 включительно.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>clickhouseSource.<br>user | **string**<br><p>Обязательное поле. Имя пользователя базы данных ClickHouse.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>clickhouseSource.<br>password | **string**<br><p>Пароль пользователя базы данных ClickHouse.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>clickhouseSource.<br>where | **string**<br><p>Критерии выбора данных в указанной таблице ClickHouse.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>mongodbSource | **object**<br>MongoDB-источник для словаря. <br>`clusters[].config.clickhouse.config.userConfig.dictionaries[]` включает только одно из полей `httpSource`, `mysqlSource`, `clickhouseSource`, `mongodbSource`, `postgresqlSource`<br><br>
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>mongodbSource.<br>db | **string**<br><p>Обязательное поле. Имя базы данных MongoDB.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>mongodbSource.<br>collection | **string**<br><p>Обязательное поле. Имя коллекции в указанной базе данных, которую следует использовать в качестве источника словаря.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>mongodbSource.<br>host | **string**<br><p>Обязательное поле. Хост MongoDB для указанной базы данных.</p> <p>Максимальная длина строки в символах — 253.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>mongodbSource.<br>port | **string** (int64)<br><p>Порт для подключения к хосту.</p> <p>Допустимые значения — от 0 до 65535 включительно.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>mongodbSource.<br>user | **string**<br><p>Обязательное поле. Имя пользователя базы данных MongoDB.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>mongodbSource.<br>password | **string**<br><p>Пароль пользователя базы данных MongoDB.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>postgresqlSource | **object**<br>PostgreSQL-источник для словаря. <br>`clusters[].config.clickhouse.config.userConfig.dictionaries[]` включает только одно из полей `httpSource`, `mysqlSource`, `clickhouseSource`, `mongodbSource`, `postgresqlSource`<br><br>
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>postgresqlSource.<br>db | **string**<br><p>Обязательное поле. Имя базы данных PostrgreSQL.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>postgresqlSource.<br>table | **string**<br><p>Обязательное поле. Имя таблицы в указанной базе данных, используемой в качестве источника словаря.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>postgresqlSource.<br>hosts[] | **string**<br><p>Обязательное поле. Имя хоста PostrgreSQL.</p> <p>Должен содержать хотя бы один элемент.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>postgresqlSource.<br>port | **string** (int64)<br><p>Порт для подключения к хосту.</p> <p>Допустимые значения — от 0 до 65535 включительно.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>postgresqlSource.<br>user | **string**<br><p>Обязательное поле. Имя пользователя базы данных PostrgreSQL.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>postgresqlSource.<br>password | **string**<br><p>Пароль пользователя базы данных PostrgreSQL.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>postgresqlSource.<br>invalidateQuery | **string**<br><p>Запрос на проверку состояния словаря, который позволит извлекать только обновленные данные. Дополнительные сведения см. в <a href="https://clickhouse.yandex/docs/ru/query_language/dicts/external_dicts_dict_lifetime/">документации ClickHouse on dictionaries</a>.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>dictionaries[].<br>postgresqlSource.<br>sslMode | **string**<br><p>Режим SSL TCP/IP соединения с хостом PostgreSQL. Дополнительные сведения см. в <a href="https://www.postgresql.org/docs/current/libpq-ssl.html">PostgreSQL documentation</a>.</p> <ul> <li>DISABLE: SSL-соединение не используется.</li> <li>ALLOW: Сначала предпринимается попытка установить незашифрованное соединение. Если это не удается, устанавливается SSL-соединение.</li> <li>PREFER: Сначала предпринимается попытка установить SSL-соединение. Если это не удается, устанавливается незашифрованное соединение.</li> <li>VERIFY_CA: Устанавливается только SSL-соединение и только при условии, что сертификат выдан доверенным центром сертификации (CA).</li> <li>VERIFY_FULL: Устанавливается только SSL-соединение и только при условии, что сертификат выдан доверенным центром сертификации и что имя хоста сервера совпадает с указанным в сертификате.</li> </ul> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>graphiteRollup[] | **object**<br><p>Параметры свертки для движка таблицы GraphiteMergeTree.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>graphiteRollup[].<br>name | **string**<br><p>Обязательное поле. Имя указанной комбинации параметров для свертки Graphite.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>graphiteRollup[].<br>patterns[] | **object**<br><p>Обязательное поле. Шаблон, используемый для свертки.</p> <p>Должен содержать хотя бы один элемент.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>graphiteRollup[].<br>patterns[].<br>regexp | **string**<br><p>Шаблон для имен метрик.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>graphiteRollup[].<br>patterns[].<br>function | **string**<br><p>Обязательное поле. Имя агрегирующей функции, которую следует применить к данным старше возраста, указанного в &quot;``retention``&quot;.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>graphiteRollup[].<br>patterns[].<br>retention[] | **object**<br><p>Обязательное поле. Возраст данных, которые следует использовать для прореживания.</p> <p>Должен содержать хотя бы один элемент.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>graphiteRollup[].<br>patterns[].<br>retention[].<br>age | **string** (int64)<br><p>Минимальный возраст данных в секундах.</p> <p>Значение должно быть больше 0.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>graphiteRollup[].<br>patterns[].<br>retention[].<br>precision | **string** (int64)<br><p>Точность определения возраста данных, в секундах.</p> <p>Значение должно быть больше 0.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>maxConnections | **integer** (int64)<br><p>Максимальное количество входящих подключений.</p> <p>Минимальное значение — 10.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>maxConcurrentQueries | **integer** (int64)<br><p>Максимальное количество одновременно обрабатываемых запросов.</p> <p>Минимальное значение — 10.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>keepAliveTimeout | **integer** (int64)<br><p>Количество миллисекунд, в течение которых ClickHouse ожидает входящие запросы прежде чем закрыть подключение.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>uncompressedCacheSize | **integer** (int64)<br><p>Размер кэша (в байтах) для несжатых данных, используемых таблицами MergeTree. См. подробное описание в <a href="https://clickhouse.yandex/docs/ru/operations/server_settings/settings/#uncompressed_cache_size">документации ClickHouse</a>.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>markCacheSize | **integer** (int64)<br><p>Примерный размер (в байтах) кэша «меток», используемых таблицами MergeTree. Подробнее в <a href="https://clickhouse.yandex/docs/ru/operations/server_settings/settings/#mark_cache_size">документации ClickHouse</a>.</p> <p>Значение должно быть больше 5368709120.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>maxTableSizeToDrop | **integer** (int64)<br><p>Максимальный размер таблицы, которую можно удалить с помощью запроса DROP. См. подробное описание в <a href="https://clickhouse.yandex/docs/ru/operations/server_settings/settings/#max_table_size_to_drop">документации ClickHouse</a>.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>maxPartitionSizeToDrop | **integer** (int64)<br><p>Максимальный размер раздела, который можно удалить с помощью запроса DROP. См. подробное описание в <a href="https://clickhouse.yandex/docs/ru/operations/server_settings/settings/#max_partition_size_to_drop">документации ClickHouse</a>.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>builtinDictionariesReloadInterval | **integer** (int64)<br><p>Параметр устарел и не имеет никакого эффекта.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>timezone | **string**<br><p>Часовой пояс сервера, используемый в преобразованиях полей DateTime. Указывается как идентификатор IANA. См. подробное описание в <a href="https://clickhouse.yandex/docs/ru/operations/server_settings/settings/#timezone">документации ClickHouse</a>.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>userConfig.<br>geobaseUri | **string**<br>
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig | **object**<br><p>Конфигурация по умолчанию для кластера ClickHouse.</p> <p>Настройки конфигурации ClickHouse. Подробное описание для каждого набора настроек доступно в <a href="https://clickhouse.yandex/docs/ru/operations/server_settings/settings/">документации ClickHouse</a>.</p> <p>Любые настройки, не перечисленные здесь, не поддерживаются.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>logLevel | **string**<br><p>Уровень логирования для кластера ClickHouse. Допустимые значения: &quot;TRACE&quot;, &quot;DEBUG&quot;, &quot;INFORMATION&quot;, &quot;WARNING&quot;, &quot;ERROR&quot;. См. описание в <a href="https://clickhouse.yandex/docs/ru/operations/server_settings/settings/#server_settings-logger">документации ClickHouse</a>.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>mergeTree | **object**<br><p>Параметры движка MergeTree. См. описание в <a href="https://clickhouse.yandex/docs/ru/operations/server_settings/settings/#merge_tree">документации ClickHouse</a>.</p> <p>Настройки движка таблицы MergeTree.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>mergeTree.<br>replicatedDeduplicationWindow | **integer** (int64)<br><p>Количество блоков хэшей, которые должен хранить ZooKeeper. Смотрите подробное описание в <a href="https://github.com/yandex/ClickHouse/blob/v18.1.0-stable/dbms/src/Storages/MergeTree/MergeTreeSettings.h#L59">ClickHouse sources</a>.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>mergeTree.<br>replicatedDeduplicationWindowSeconds | **integer** (int64)<br><p>Период времени, в течение которого следует хранить блоки хэшей. См. описание в <a href="https://github.com/yandex/ClickHouse/blob/v18.1.0-stable/dbms/src/Storages/MergeTree/MergeTreeSettings.h#L64">ClickHouse sources</a>.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>mergeTree.<br>partsToDelayInsert | **integer** (int64)<br>
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>mergeTree.<br>partsToThrowInsert | **integer** (int64)<br>
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>mergeTree.<br>maxReplicatedMergesInQueue | **integer** (int64)<br>
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>mergeTree.<br>numberOfFreeEntriesInPoolToLowerMaxSizeOfMerge | **integer** (int64)<br>
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>mergeTree.<br>maxBytesToMergeAtMinSpaceInPool | **integer** (int64)<br>
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>compression[] | **object**<br><p>Параметры сжатия для кластера ClickHouse. См. подробное описание в <a href="https://clickhouse.yandex/docs/ru/operations/server_settings/settings/#compression">документации ClickHouse</a>.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>compression[].<br>method | **string**<br><p>Метод сжатия, используемый для указанной комбинации &quot;min_part_size&quot; и &quot;min_part_size_ratio&quot;.</p> <ul> <li>LZ4: <a href="https://lz4.github.io/lz4/">LZ4 compression algorithm</a>.</li> <li>ZSTD: <a href="https://facebook.github.io/zstd/">Zstandard compression algorithm</a>.</li> </ul> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>compression[].<br>minPartSize | **string** (int64)<br><p>Минимальный размер части таблицы.</p> <p>Минимальное значение — 1.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>compression[].<br>minPartSizeRatio | **number** (double)<br><p>Минимальное отношение части к размеру всех данных в таблице.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[] | **object**<br><p>Конфигурация внешних словарей для кластера ClickHouse. См. подробное описание в <a href="https://clickhouse.yandex/docs/ru/query_language/dicts/external_dicts/">документации ClickHouse</a>.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>name | **string**<br><p>Обязательное поле. Имя внешнего словаря.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>structure | **object**<br>Обязательное поле. Набор атрибутов внешнего словаря. Подробное описание см. в [документации ClickHouse](https://clickhouse.yandex/docs/ru/query_language/dicts/external_dicts_dict_structure/).<br>
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>structure.<br>id | **object**<br><p>Один столбец с числовыми ключами для словаря.</p> <p>Числовой ключ.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>structure.<br>id.<br>name | **string**<br><p>Обязательное поле. Имя числового ключа.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>structure.<br>key | **object**<br><p>Составной ключ для словаря, содержащего один или несколько столбцов с ключами. Подробнее см. в <a href="https://clickhouse.yandex/docs/ru/query_language/dicts/external_dicts_dict_structure/#composite-key">документации ClickHouse</a>.</p> <p>Составной ключ.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>structure.<br>key.<br>attributes[] | **object**<br><p>Обязательное поле. Поля составного ключа.</p> <p>Должен содержать хотя бы один элемент.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>structure.<br>key.<br>attributes[].<br>name | **string**<br><p>Обязательное поле. Имя столбца.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>structure.<br>key.<br>attributes[].<br>type | **string**<br><p>Обязательное поле. Тип столбца.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>structure.<br>key.<br>attributes[].<br>nullValue | **string**<br><p>Значение по умолчанию для элемента без данных (например, пустая строка).</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>structure.<br>key.<br>attributes[].<br>expression | **string**<br><p>Выражение, описывающее атрибут, если применимо.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>structure.<br>key.<br>attributes[].<br>hierarchical | **boolean** (boolean)<br><p>Признак поддержки иерархии. Значение по умолчанию &quot;false&quot;.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>structure.<br>key.<br>attributes[].<br>injective | **boolean** (boolean)<br><p>Признакт инъективного отображения &quot;id -&gt; атрибут&quot;. Значение по умолчанию &quot;false&quot;.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>structure.<br>rangeMin | **object**<br><p>Поле, содержащее начало диапазона для словарей, которые хранятся в памяти способом &quot;RANGE_HASHED&quot;. Подробнее см.<a href="https://clickhouse.yandex/docs/ru/query_language/dicts/external_dicts_dict_layout/#range-hashed">документации ClickHouse</a></p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>structure.<br>rangeMin.<br>name | **string**<br><p>Обязательное поле. Имя столбца.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>structure.<br>rangeMin.<br>type | **string**<br><p>Обязательное поле. Тип столбца.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>structure.<br>rangeMin.<br>nullValue | **string**<br><p>Значение по умолчанию для элемента без данных (например, пустая строка).</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>structure.<br>rangeMin.<br>expression | **string**<br><p>Выражение, описывающее атрибут, если применимо.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>structure.<br>rangeMin.<br>hierarchical | **boolean** (boolean)<br><p>Признак поддержки иерархии. Значение по умолчанию &quot;false&quot;.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>structure.<br>rangeMin.<br>injective | **boolean** (boolean)<br><p>Признакт инъективного отображения &quot;id -&gt; атрибут&quot;. Значение по умолчанию &quot;false&quot;.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>structure.<br>rangeMax | **object**<br><p>Поле, содержащее конец диапазона для словарей, которые хранятся в памяти способом &quot;RANGE_HASHED&quot;. Подробнее см.<a href="https://clickhouse.yandex/docs/ru/query_language/dicts/external_dicts_dict_layout/#range-hashed">документации ClickHouse</a></p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>structure.<br>rangeMax.<br>name | **string**<br><p>Обязательное поле. Имя столбца.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>structure.<br>rangeMax.<br>type | **string**<br><p>Обязательное поле. Тип столбца.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>structure.<br>rangeMax.<br>nullValue | **string**<br><p>Значение по умолчанию для элемента без данных (например, пустая строка).</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>structure.<br>rangeMax.<br>expression | **string**<br><p>Выражение, описывающее атрибут, если применимо.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>structure.<br>rangeMax.<br>hierarchical | **boolean** (boolean)<br><p>Признак поддержки иерархии. Значение по умолчанию &quot;false&quot;.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>structure.<br>rangeMax.<br>injective | **boolean** (boolean)<br><p>Признакт инъективного отображения &quot;id -&gt; атрибут&quot;. Значение по умолчанию &quot;false&quot;.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>structure.<br>attributes[] | **object**<br><p>Обязательное поле. Описание полей, доступных для запросов к базе данных. Подробнее см. в <a href="https://clickhouse.yandex/docs/ru/query_language/dicts/external_dicts_dict_structure/#attributes">документации ClickHouse</a>.</p> <p>Должен содержать хотя бы один элемент.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>structure.<br>attributes[].<br>name | **string**<br><p>Обязательное поле. Имя столбца.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>structure.<br>attributes[].<br>type | **string**<br><p>Обязательное поле. Тип столбца.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>structure.<br>attributes[].<br>nullValue | **string**<br><p>Значение по умолчанию для элемента без данных (например, пустая строка).</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>structure.<br>attributes[].<br>expression | **string**<br><p>Выражение, описывающее атрибут, если применимо.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>structure.<br>attributes[].<br>hierarchical | **boolean** (boolean)<br><p>Признак поддержки иерархии. Значение по умолчанию &quot;false&quot;.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>structure.<br>attributes[].<br>injective | **boolean** (boolean)<br><p>Признакт инъективного отображения &quot;id -&gt; атрибут&quot;. Значение по умолчанию &quot;false&quot;.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>layout | **object**<br>Обязательное поле. Макет для хранения словаря в памяти. Подробное описание см. в [документации ClickHouse](https://clickhouse.yandex/docs/ru/query_language/dicts/external_dicts_dict_layout/).<br><p>Макет, определяющий способ хранения словаря в памяти.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>layout.<br>type | **string**<br><p>Обязательное поле. Тип макета для внешнего словаря.</p> <ul> <li>FLAT: Весь словарь хранится в памяти в виде плоских массивов. Доступно для любых источников словарей.</li> <li>HASHED: Весь словарь хранится в памяти в виде хэш-таблицы. Доступно для любых источников словарей.</li> <li>COMPLEX_KEY_HASHED: Аналогичен HASHED, для использования с составными ключами. Доступно для любых источников словарей.</li> <li>RANGE_HASHED: Весь словарь хранится в памяти в виде хэш-таблицы, с упорядоченным массивом диапазонов и соответствующих им значений. Доступно для любых источников словарей.</li> <li>CACHE: Словарь хранится в кэше с заданным количеством ячеек. Доступно для источников словарей MySQL, ClickHouse и HTTP.</li> <li>COMPLEX_KEY_CACHE: Аналогичен CACHE, для использования с составными ключами. Доступно для источников словарей MySQL, ClickHouse и HTTP.</li> </ul> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>layout.<br>sizeInCells | **string** (int64)<br><p>Количество ячеек в кэше. Округляется до степени двойки. Применимо только для типов макета CACHE и COMPLEX_KEY_CACHE.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>fixedLifetime | **string** (int64) <br>`clusters[].config.clickhouse.config.defaultConfig.dictionaries[]` включает только одно из полей `fixedLifetime`, `lifetimeRange`<br><br><p>Жесткий интервал между обновлениями словаря.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>lifetimeRange | **object**<br>Диапазон интервалов между обновлениями словаря, из которых может выбирать ClickHouse. <br>`clusters[].config.clickhouse.config.defaultConfig.dictionaries[]` включает только одно из полей `fixedLifetime`, `lifetimeRange`<br><br>
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>lifetimeRange.<br>min | **string** (int64)<br><p>Минимальное время жизни словаря.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>lifetimeRange.<br>max | **string** (int64)<br><p>Максимальное время жизни словаря.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>httpSource | **object**<br>HTTP-источник для словаря. <br>`clusters[].config.clickhouse.config.defaultConfig.dictionaries[]` включает только одно из полей `httpSource`, `mysqlSource`, `clickhouseSource`, `mongodbSource`, `postgresqlSource`<br><br>
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>httpSource.<br>url | **string**<br><p>Обязательное поле. URL внешнего словаря, доступного по HTTP.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>httpSource.<br>format | **string**<br><p>Обязательное поле. Формат данных. Допустимые значения: все форматы, поддерживаемые диалектом ClickHouse SQL.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>mysqlSource | **object**<br>MySQL-источник для словаря. <br>`clusters[].config.clickhouse.config.defaultConfig.dictionaries[]` включает только одно из полей `httpSource`, `mysqlSource`, `clickhouseSource`, `mongodbSource`, `postgresqlSource`<br><br>
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>mysqlSource.<br>db | **string**<br><p>Обязательное поле. Имя базы данных MySQL, к которой нужно подключаться.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>mysqlSource.<br>table | **string**<br><p>Обязательное поле. Имя таблицы базы данных, которую следует использовать в качестве словаря ClickHouse.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>mysqlSource.<br>port | **string** (int64)<br><p>Порт по умолчанию, который нужно использовать при подключении к реплике источника словаря.</p> <p>Допустимые значения — от 0 до 65535 включительно.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>mysqlSource.<br>user | **string**<br><p>Имя пользователя по умолчанию для реплик источника словаря.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>mysqlSource.<br>password | **string**<br><p>Пароль пользователя по умолчанию для реплик источника словаря.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>mysqlSource.<br>replicas[] | **object**<br><p>Обязательное поле. Список реплик базы данных MySQL, используемой в качестве источника словаря.</p> <p>Должен содержать хотя бы один элемент.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>mysqlSource.<br>replicas[].<br>host | **string**<br><p>Обязательное поле. Хост реплики MySQL.</p> <p>Максимальная длина строки в символах — 253.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>mysqlSource.<br>replicas[].<br>priority | **string** (int64)<br><p>Обязательное поле. Приоритет реплики, который ClickHouse должен учитывать при подключении. Реплике с наивысшим приоритетом должно соответствовать наименьшее значение в этом поле.</p> <p>Значение должно быть больше 0.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>mysqlSource.<br>replicas[].<br>port | **string** (int64)<br><p>Порт, который нужно использовать при подключении к реплике. Если для какой-либо реплики не указан порт, ClickHouse использует порт, указанный для источника.</p> <p>Допустимые значения — от 0 до 65535 включительно.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>mysqlSource.<br>replicas[].<br>user | **string**<br><p>Имя пользователя базы данных MySQL.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>mysqlSource.<br>replicas[].<br>password | **string**<br><p>Пароль пользователя базы данных MySQL.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>mysqlSource.<br>where | **string**<br><p>Критерии выбора данных в указанной таблице MySQL.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>mysqlSource.<br>invalidateQuery | **string**<br><p>Запрос на проверку состояния словаря, который позволит извлекать только обновленные данные. Дополнительные сведения см. в <a href="https://clickhouse.yandex/docs/ru/query_language/dicts/external_dicts_dict_lifetime/">документации ClickHouse on dictionaries</a>.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>clickhouseSource | **object**<br>ClickHouse-источник для словаря. <br>`clusters[].config.clickhouse.config.defaultConfig.dictionaries[]` включает только одно из полей `httpSource`, `mysqlSource`, `clickhouseSource`, `mongodbSource`, `postgresqlSource`<br><br>
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>clickhouseSource.<br>db | **string**<br><p>Обязательное поле. Имя базы данных ClickHouse.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>clickhouseSource.<br>table | **string**<br><p>Обязательное поле. Имя таблицы в указанной базе данных, используемой в качестве источника словаря.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>clickhouseSource.<br>host | **string**<br><p>Обязательное поле. Хост ClickHouse для указанной базы данных.</p> <p>Максимальная длина строки в символах — 253.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>clickhouseSource.<br>port | **string** (int64)<br><p>Порт для подключения к хосту.</p> <p>Допустимые значения — от 0 до 65535 включительно.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>clickhouseSource.<br>user | **string**<br><p>Обязательное поле. Имя пользователя базы данных ClickHouse.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>clickhouseSource.<br>password | **string**<br><p>Пароль пользователя базы данных ClickHouse.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>clickhouseSource.<br>where | **string**<br><p>Критерии выбора данных в указанной таблице ClickHouse.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>mongodbSource | **object**<br>MongoDB-источник для словаря. <br>`clusters[].config.clickhouse.config.defaultConfig.dictionaries[]` включает только одно из полей `httpSource`, `mysqlSource`, `clickhouseSource`, `mongodbSource`, `postgresqlSource`<br><br>
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>mongodbSource.<br>db | **string**<br><p>Обязательное поле. Имя базы данных MongoDB.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>mongodbSource.<br>collection | **string**<br><p>Обязательное поле. Имя коллекции в указанной базе данных, которую следует использовать в качестве источника словаря.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>mongodbSource.<br>host | **string**<br><p>Обязательное поле. Хост MongoDB для указанной базы данных.</p> <p>Максимальная длина строки в символах — 253.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>mongodbSource.<br>port | **string** (int64)<br><p>Порт для подключения к хосту.</p> <p>Допустимые значения — от 0 до 65535 включительно.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>mongodbSource.<br>user | **string**<br><p>Обязательное поле. Имя пользователя базы данных MongoDB.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>mongodbSource.<br>password | **string**<br><p>Пароль пользователя базы данных MongoDB.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>postgresqlSource | **object**<br>PostgreSQL-источник для словаря. <br>`clusters[].config.clickhouse.config.defaultConfig.dictionaries[]` включает только одно из полей `httpSource`, `mysqlSource`, `clickhouseSource`, `mongodbSource`, `postgresqlSource`<br><br>
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>postgresqlSource.<br>db | **string**<br><p>Обязательное поле. Имя базы данных PostrgreSQL.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>postgresqlSource.<br>table | **string**<br><p>Обязательное поле. Имя таблицы в указанной базе данных, используемой в качестве источника словаря.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>postgresqlSource.<br>hosts[] | **string**<br><p>Обязательное поле. Имя хоста PostrgreSQL.</p> <p>Должен содержать хотя бы один элемент.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>postgresqlSource.<br>port | **string** (int64)<br><p>Порт для подключения к хосту.</p> <p>Допустимые значения — от 0 до 65535 включительно.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>postgresqlSource.<br>user | **string**<br><p>Обязательное поле. Имя пользователя базы данных PostrgreSQL.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>postgresqlSource.<br>password | **string**<br><p>Пароль пользователя базы данных PostrgreSQL.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>postgresqlSource.<br>invalidateQuery | **string**<br><p>Запрос на проверку состояния словаря, который позволит извлекать только обновленные данные. Дополнительные сведения см. в <a href="https://clickhouse.yandex/docs/ru/query_language/dicts/external_dicts_dict_lifetime/">документации ClickHouse on dictionaries</a>.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>dictionaries[].<br>postgresqlSource.<br>sslMode | **string**<br><p>Режим SSL TCP/IP соединения с хостом PostgreSQL. Дополнительные сведения см. в <a href="https://www.postgresql.org/docs/current/libpq-ssl.html">PostgreSQL documentation</a>.</p> <ul> <li>DISABLE: SSL-соединение не используется.</li> <li>ALLOW: Сначала предпринимается попытка установить незашифрованное соединение. Если это не удается, устанавливается SSL-соединение.</li> <li>PREFER: Сначала предпринимается попытка установить SSL-соединение. Если это не удается, устанавливается незашифрованное соединение.</li> <li>VERIFY_CA: Устанавливается только SSL-соединение и только при условии, что сертификат выдан доверенным центром сертификации (CA).</li> <li>VERIFY_FULL: Устанавливается только SSL-соединение и только при условии, что сертификат выдан доверенным центром сертификации и что имя хоста сервера совпадает с указанным в сертификате.</li> </ul> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>graphiteRollup[] | **object**<br><p>Параметры свертки для движка таблицы GraphiteMergeTree.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>graphiteRollup[].<br>name | **string**<br><p>Обязательное поле. Имя указанной комбинации параметров для свертки Graphite.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>graphiteRollup[].<br>patterns[] | **object**<br><p>Обязательное поле. Шаблон, используемый для свертки.</p> <p>Должен содержать хотя бы один элемент.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>graphiteRollup[].<br>patterns[].<br>regexp | **string**<br><p>Шаблон для имен метрик.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>graphiteRollup[].<br>patterns[].<br>function | **string**<br><p>Обязательное поле. Имя агрегирующей функции, которую следует применить к данным старше возраста, указанного в &quot;``retention``&quot;.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>graphiteRollup[].<br>patterns[].<br>retention[] | **object**<br><p>Обязательное поле. Возраст данных, которые следует использовать для прореживания.</p> <p>Должен содержать хотя бы один элемент.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>graphiteRollup[].<br>patterns[].<br>retention[].<br>age | **string** (int64)<br><p>Минимальный возраст данных в секундах.</p> <p>Значение должно быть больше 0.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>graphiteRollup[].<br>patterns[].<br>retention[].<br>precision | **string** (int64)<br><p>Точность определения возраста данных, в секундах.</p> <p>Значение должно быть больше 0.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>maxConnections | **integer** (int64)<br><p>Максимальное количество входящих подключений.</p> <p>Минимальное значение — 10.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>maxConcurrentQueries | **integer** (int64)<br><p>Максимальное количество одновременно обрабатываемых запросов.</p> <p>Минимальное значение — 10.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>keepAliveTimeout | **integer** (int64)<br><p>Количество миллисекунд, в течение которых ClickHouse ожидает входящие запросы прежде чем закрыть подключение.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>uncompressedCacheSize | **integer** (int64)<br><p>Размер кэша (в байтах) для несжатых данных, используемых таблицами MergeTree. См. подробное описание в <a href="https://clickhouse.yandex/docs/ru/operations/server_settings/settings/#uncompressed_cache_size">документации ClickHouse</a>.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>markCacheSize | **integer** (int64)<br><p>Примерный размер (в байтах) кэша «меток», используемых таблицами MergeTree. Подробнее в <a href="https://clickhouse.yandex/docs/ru/operations/server_settings/settings/#mark_cache_size">документации ClickHouse</a>.</p> <p>Значение должно быть больше 5368709120.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>maxTableSizeToDrop | **integer** (int64)<br><p>Максимальный размер таблицы, которую можно удалить с помощью запроса DROP. См. подробное описание в <a href="https://clickhouse.yandex/docs/ru/operations/server_settings/settings/#max_table_size_to_drop">документации ClickHouse</a>.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>maxPartitionSizeToDrop | **integer** (int64)<br><p>Максимальный размер раздела, который можно удалить с помощью запроса DROP. См. подробное описание в <a href="https://clickhouse.yandex/docs/ru/operations/server_settings/settings/#max_partition_size_to_drop">документации ClickHouse</a>.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>builtinDictionariesReloadInterval | **integer** (int64)<br><p>Параметр устарел и не имеет никакого эффекта.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>timezone | **string**<br><p>Часовой пояс сервера, используемый в преобразованиях полей DateTime. Указывается как идентификатор IANA. См. подробное описание в <a href="https://clickhouse.yandex/docs/ru/operations/server_settings/settings/#timezone">документации ClickHouse</a>.</p> 
clusters[].<br>config.<br>clickhouse.<br>config.<br>defaultConfig.<br>geobaseUri | **string**<br>
clusters[].<br>config.<br>clickhouse.<br>resources | **object**<br><p>Ресурсы, выделенные хостам ClickHouse.</p> 
clusters[].<br>config.<br>clickhouse.<br>resources.<br>resourcePresetId | **string**<br><p>Идентификатор набора вычислительных ресурсов, доступных хосту (процессор, память и т. д.). Все доступные наборы ресурсов перечислены в <a href="/docs/managed-clickhouse/concepts/instance-types">документации</a>.</p> 
clusters[].<br>config.<br>clickhouse.<br>resources.<br>diskSize | **string** (int64)<br><p>Объем хранилища, доступного хосту, в байтах.</p> 
clusters[].<br>config.<br>clickhouse.<br>resources.<br>diskTypeId | **string**<br><p>Тип хранилища для хоста. Возможные значения:</p> <ul> <li>network-hdd — сетевой HDD-диск;</li> <li>network-ssd — сетевой SSD-диск;</li> <li>local-ssd — локальное SSD-хранилище.</li> </ul> 
clusters[].<br>config.<br>zookeeper | **object**<br><p>Конфигурация и распределение ресурсов для хостов ZooKeeper.</p> 
clusters[].<br>config.<br>zookeeper.<br>resources | **object**<br><p>Ресурсы, выделенные хостам ZooKeeper.</p> 
clusters[].<br>config.<br>zookeeper.<br>resources.<br>resourcePresetId | **string**<br><p>Идентификатор набора вычислительных ресурсов, доступных хосту (процессор, память и т. д.). Все доступные наборы ресурсов перечислены в <a href="/docs/managed-clickhouse/concepts/instance-types">документации</a>.</p> 
clusters[].<br>config.<br>zookeeper.<br>resources.<br>diskSize | **string** (int64)<br><p>Объем хранилища, доступного хосту, в байтах.</p> 
clusters[].<br>config.<br>zookeeper.<br>resources.<br>diskTypeId | **string**<br><p>Тип хранилища для хоста. Возможные значения:</p> <ul> <li>network-hdd — сетевой HDD-диск;</li> <li>network-ssd — сетевой SSD-диск;</li> <li>local-ssd — локальное SSD-хранилище.</li> </ul> 
clusters[].<br>config.<br>backupWindowStart | **object**<br><p>Время запуска ежедневного резервного копирования, в часовом поясе UTC.</p> <p>Время суток. Дата и часовой пояс либо не учитываются, либо задаются в других местах.</p> <p>API может разрешить использование високосной секунды.</p> <p>Связанные типы: <a href="https://github.com/googleapis/googleapis/blob/master/google/type/date.proto">google.type.Date</a> и <a href="https://github.com/protocolbuffers/protobuf/blob/master/src/google/protobuf/timestamp.proto">google.protobuf.Timestamp</a>.</p> 
clusters[].<br>config.<br>backupWindowStart.<br>hours | **integer** (int32)<br><p>Часы. Допустимые значения: от 0 до 23.</p> <p>API может разрешить использовать значение в формате &quot;24:00:00&quot; в требующих этого сценариях (например, для указания времени закрытия учреждения).</p> 
clusters[].<br>config.<br>backupWindowStart.<br>minutes | **integer** (int32)<br><p>Минуты. Допустимые значения: от 0 до 59.</p> 
clusters[].<br>config.<br>backupWindowStart.<br>seconds | **integer** (int32)<br><p>Секунды. Стандартные допустимые значения: от 0 до 59.</p> <p>API может разрешить использовать значение 60, если также разрешено использование високосной секунды.</p> 
clusters[].<br>config.<br>backupWindowStart.<br>nanos | **integer** (int32)<br><p>Доли секунды (в наносекундах). Допустимые значения: от 0 до 999999999.</p> 
clusters[].<br>config.<br>access | **object**<br><p>Политика доступа для внешних сервисов.</p> 
clusters[].<br>config.<br>access.<br>dataLens | **boolean** (boolean)<br><p>Разрешить экспорт данных из кластера в Yandex DataLens.</p> 
clusters[].<br>config.<br>access.<br>webSql | **boolean** (boolean)<br><p>Разрешить SQL-запросы к базам данных кластера из консоли управления облаком.</p> <p>Подробнее см. в <a href="/docs/managed-clickhouse/operations/web-sql-query">SQL-запросы в консоли управления</a>.</p> 
clusters[].<br>config.<br>access.<br>metrika | **boolean** (boolean)<br><p>Разрешить импорт данных из Яндекс Метрики и AppMetrica в кластер.</p> <p>Подробнее см. в <a href="https://appmetrica.yandex.ru/docs/common/cloud/about.html">Экспорт данных в {{ yandex-cloud }}</a>.</p> 
clusters[].<br>config.<br>access.<br>serverless | **boolean** (boolean)<br><p>Разрешить доступ к кластеру для Serverless.</p> 
clusters[].<br>networkId | **string**<br><p>Идентификатор сети, к которой принадлежит кластер.</p> 
clusters[].<br>health | **string**<br><p>Здоровье кластера.</p> <ul> <li>HEALTH_UNKNOWN: Состояние кластера неизвестно (``health`` для каждого хоста в кластере — UNKNOWN).</li> <li>ALIVE: Кластер работает нормально (``health`` для каждого хоста в кластере — ALIVE).</li> <li>DEAD: Кластер не работает (``health`` для каждого хоста в кластере — DEAD).</li> <li>DEGRADED: Кластер работает неоптимально (``health`` по крайней мере для одного хоста в кластере не ALIVE).</li> </ul> 
clusters[].<br>status | **string**<br><p>Текущее состояние кластера.</p> <ul> <li>STATUS_UNKNOWN: Состояние кластера неизвестно.</li> <li>CREATING: Кластер создается.</li> <li>RUNNING: Кластер работает нормально.</li> <li>ERROR: В кластере произошла ошибка, блокирующая работу.</li> <li>UPDATING: Кластер изменяется.</li> <li>STOPPING: Кластер останавливается.</li> <li>STOPPED: Кластер остановлен.</li> <li>STARTING: Кластер запускается.</li> </ul> 
clusters[].<br>serviceAccountId | **string**<br><p>Идентификатор сервисного аккаунта, используемого для доступа к Yandex Object Storage.</p> 
nextPageToken | **string**<br><p>Токен для получения следующей страницы результатов в ответе. Если количество результатов больше чем <a href="/docs/managed-clickhouse/api-ref/Cluster/list#query_params">pageSize</a>, используйте <a href="/docs/managed-clickhouse/api-ref/Cluster/list#responses">nextPageToken</a> в качестве значения параметра <a href="/docs/managed-clickhouse/api-ref/Cluster/list#query_params">pageToken</a> в следующем запросе. Все последующие запросы будут получать свои значения <a href="/docs/managed-clickhouse/api-ref/Cluster/list#responses">nextPageToken</a> для перебора страниц результатов.</p> 