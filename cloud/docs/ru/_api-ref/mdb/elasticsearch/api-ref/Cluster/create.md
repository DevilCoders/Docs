---
editable: false
---

# Метод create
Создает новый кластер Elasticsearch в указанном каталоге.
 

 
## HTTP-запрос {#https-request}
```
POST https://mdb.api.cloud.yandex.net/managed-elasticsearch/v1/clusters
```
 
## Параметры в теле запроса {#body_params}
 
```json 
{
  "folderId": "string",
  "name": "string",
  "description": "string",
  "labels": "object",
  "environment": "string",
  "configSpec": {
    "version": "string",
    "elasticsearchSpec": {
      "dataNode": {
        "resources": {
          "resourcePresetId": "string",
          "diskSize": "string",
          "diskTypeId": "string"
        },
        "elasticsearchConfig_7_6": {
          "fielddataCacheSize": "integer",
          "maxClauseCount": "integer"
        }
      },
      "masterNode": {
        "resources": {
          "resourcePresetId": "string",
          "diskSize": "string",
          "diskTypeId": "string"
        }
      }
    }
  },
  "userSpecs": [
    {
      "name": "string",
      "password": "string"
    }
  ],
  "hostSpecs": [
    {
      "zoneId": "string",
      "subnetId": "string",
      "assignPublicIp": true,
      "type": "string",
      "shardName": "string"
    }
  ],
  "networkId": "string"
}
```

 
Поле | Описание
--- | ---
folderId | **string**<br><p>Обязательное поле. Идентификатор каталога, в котором будет создан кластер Elasticsearch.</p> <p>Максимальная длина строки в символах — 50.</p> 
name | **string**<br><p>Обязательное поле. Имя кластера Elasticsearch. Имя должно быть уникальным в рамках каталога.</p> <p>Максимальная длина строки в символах — 63. Значение должно соответствовать регулярному выражению ``[a-zA-Z0-9_-]*``.</p> 
description | **string**<br><p>Описание кластера Elasticsearch.</p> <p>Максимальная длина строки в символах — 256.</p> 
labels | **object**<br><p>Пользовательские метки для кластера Elasticsearch в виде пар ``key:value``.</p> <p>Например, &quot;project&quot;: &quot;mvp&quot; или &quot;source&quot;: &quot;dictionary&quot;.</p> <p>Не более 64 на ресурс. Длина строки в символах для каждого ключа должна быть от 1 до 63. Каждый ключ должен соответствовать регулярному выражению ``[a-z][-_0-9a-z]*``. Максимальная длина строки в символах для каждого значения — 63. Каждое значение должно соответствовать регулярному выражению ``[-_0-9a-z]*``.</p> 
environment | **string**<br><p>Среда развертывания кластера Elasticsearch.</p> <ul> <li>PRODUCTION: стабильная среда с осторожной политикой обновления — во время регулярного обслуживания применяются только срочные исправления.</li> <li>PRESTABLE: среда с более агрессивной политикой обновления — новые версии развертываются независимо от обратной совместимости.</li> </ul> 
configSpec | **object**<br><p>Обязательное поле. Конфигурация Elasticsearch и хостов для кластера.</p> 
configSpec.<br>version | **string**<br><p>Версия Elasticsearch.</p> 
configSpec.<br>elasticsearchSpec | **object**<br><p>Конфигурация и распределение ресурсов для узлов Elasticsearch.</p> 
configSpec.<br>elasticsearchSpec.<br>dataNode | **object**<br><p>Конфигурация и распределение ресурсов для узлов Elasticsearch с ролью Data node.</p> 
configSpec.<br>elasticsearchSpec.<br>dataNode.<br>resources | **object**<br>Ресурсы, выделенные узлам Elasticsearch с ролью Data node.<br>
configSpec.<br>elasticsearchSpec.<br>dataNode.<br>resources.<br>resourcePresetId | **string**<br><p>Идентификатор набора вычислительных ресурсов, доступных хосту (процессор, память и т.д.). Все доступные наборы ресурсов перечислены в <a href="/docs/managed-elasticsearch/concepts/instance-types">документации</a>.</p> 
configSpec.<br>elasticsearchSpec.<br>dataNode.<br>resources.<br>diskSize | **string** (int64)<br><p>Объем хранилища, доступного хосту, в байтах.</p> 
configSpec.<br>elasticsearchSpec.<br>dataNode.<br>resources.<br>diskTypeId | **string**<br><p>Тип хранилища для хоста. Все доступные типы перечислены в <a href="/docs/managed-elasticsearch/concepts/storage">документации</a>.</p> 
configSpec.<br>elasticsearchSpec.<br>dataNode.<br>elasticsearchConfig_7_6 | **object**<br><p>Здесь перечислены поддерживаемые параметры конфигурации Elasticsearch 7.6.</p> <p>Подробное описание всех параметров доступно в <a href="https://www.elastic.co/guide/en/elasticsearch/reference/current/index.html">документации Elasticsearch</a>.</p> <p>Любые параметры, не перечисленные здесь, не поддерживаются.</p> 
configSpec.<br>elasticsearchSpec.<br>dataNode.<br>elasticsearchConfig_7_6.<br>fielddataCacheSize | **integer** (int64)<br><p>Максимальный процент от общего объема кучи (heap), который может выделяться под кэш данных в полях.</p> <p>Все значения полей, помещенные в этот кэш, загружаются в память для обеспечения быстрого доступа к этим значениям при работе с документами. Построение кэша данных для поля — затратная операция, поэтому рекомендуется иметь достаточный объем памяти для этого кэша и поддерживать его в заполненном состоянии.</p> <p>Значение по умолчанию: не ограничено.</p> <p>См. подробное описание в <a href="https://www.elastic.co/guide/en/elasticsearch/reference/current/modules-fielddata.html">документации Elasticsearch</a>.</p> 
configSpec.<br>elasticsearchSpec.<br>dataNode.<br>elasticsearchConfig_7_6.<br>maxClauseCount | **integer** (int64)<br><p>Максимальное число выражений, которое может содержаться в булевом запросе (bool query).</p> <p>Эта настройка позволяет не допустить разрастания поисковых запросов до больших размеров, чтобы запросы не потребляли много памяти и ресурсов процессора. Настройка влияет не только на запросы типа ``bool``, но и на многие другие запросы, которые неявно преобразуются Elasticsearch в запросы типа ``bool``.</p> <p>Значение по умолчанию: ``1024``.</p> <p>См. подробное описание в <a href="https://www.elastic.co/guide/en/elasticsearch/reference/current/search-settings.html">документации Elasticsearch</a>.</p> 
configSpec.<br>elasticsearchSpec.<br>masterNode | **object**<br><p>Конфигурация и распределение ресурсов для узлов Elasticsearch с ролью Master node.</p> 
configSpec.<br>elasticsearchSpec.<br>masterNode.<br>resources | **object**<br><p>Ресурсы, выделенные узлам Elasticsearch с ролью Master node.</p> 
configSpec.<br>elasticsearchSpec.<br>masterNode.<br>resources.<br>resourcePresetId | **string**<br><p>Идентификатор набора вычислительных ресурсов, доступных хосту (процессор, память и т.д.). Все доступные наборы ресурсов перечислены в <a href="/docs/managed-elasticsearch/concepts/instance-types">документации</a>.</p> 
configSpec.<br>elasticsearchSpec.<br>masterNode.<br>resources.<br>diskSize | **string** (int64)<br><p>Объем хранилища, доступного хосту, в байтах.</p> 
configSpec.<br>elasticsearchSpec.<br>masterNode.<br>resources.<br>diskTypeId | **string**<br><p>Тип хранилища для хоста. Все доступные типы перечислены в <a href="/docs/managed-elasticsearch/concepts/storage">документации</a>.</p> 
userSpecs[] | **object**<br><p>Обязательное поле. Одно или несколько описаний пользователей, которых нужно создать в кластере Elasticsearch.</p> <p>Должен содержать хотя бы один элемент.</p> 
userSpecs[].<br>name | **string**<br><p>Обязательное поле. Имя пользователя Elasticsearch.</p> <p>Максимальная длина строки в символах — 63. Значение должно соответствовать регулярному выражению ``[a-zA-Z0-9_]*``.</p> 
userSpecs[].<br>password | **string**<br><p>Обязательное поле. Пароль пользователя Elasticsearch.</p> <p>Длина строки в символах должна быть от 8 до 128.</p> 
hostSpecs[] | **object**<br><p>Обязательное поле. Одна или несколько конфигураций хостов, создаваемых в кластере Elasticsearch.</p> <p>Должен содержать хотя бы один элемент.</p> 
hostSpecs[].<br>zoneId | **string**<br><p>Идентификатор зоны доступности, в которой находится хост.</p> <p>Максимальная длина строки в символах — 50.</p> 
hostSpecs[].<br>subnetId | **string**<br><p>Идентификатор подсети, в которой находится хост.</p> <p>Максимальная длина строки в символах — 50.</p> 
hostSpecs[].<br>assignPublicIp | **boolean** (boolean)<br><p>Флаг, определяющий, назначен ли хосту публичный IP-адрес.</p> <p>Если значение равно ``true``, то этот хост доступен в Интернете через его публичный IP-адрес.</p> 
hostSpecs[].<br>type | **string**<br><p>Обязательное поле. Тип хоста.</p> <ul> <li>DATA_NODE: этот хост является узлом Elasticsearch с ролью Data node.</li> <li>MASTER_NODE: этот хост является узлом Elasticsearch с ролью Master node.</li> </ul> 
hostSpecs[].<br>shardName | **string**<br><p>Имя шарда, который нужно создать на хосте.</p> <p>Максимальная длина строки в символах — 63. Значение должно соответствовать регулярному выражению ``[a-zA-Z0-9_-]*``.</p> 
networkId | **string**<br><p>Обязательное поле. Идентификатор сети, в которой будет создан кластер Elasticsearch.</p> <p>Максимальная длина строки в символах — 50.</p> 
 
## Ответ {#responses}
**HTTP Code: 200 - OK**

```json 
{
  "id": "string",
  "description": "string",
  "createdAt": "string",
  "createdBy": "string",
  "modifiedAt": "string",
  "done": true,
  "metadata": "object",

  //  включает только одно из полей `error`, `response`
  "error": {
    "code": "integer",
    "message": "string",
    "details": [
      "object"
    ]
  },
  "response": "object",
  // конец списка возможных полей

}
```
Ресурс Operation. Дополнительные сведения см. в разделе
[Объект Operation](/docs/api-design-guide/concepts/operation).
 
Поле | Описание
--- | ---
id | **string**<br><p>Идентификатор операции.</p> 
description | **string**<br><p>Описание операции. Длина описания должна быть от 0 до 256 символов.</p> 
createdAt | **string** (date-time)<br><p>Время создания ресурса в формате в <a href="https://www.ietf.org/rfc/rfc3339.txt">RFC3339</a>.</p> <p>Строка в формате <a href="https://www.ietf.org/rfc/rfc3339.txt">RFC3339</a>.</p> 
createdBy | **string**<br><p>Идентификатор пользователя или сервисного аккаунта, инициировавшего операцию.</p> 
modifiedAt | **string** (date-time)<br><p>Время, когда ресурс Operation последний раз обновлялся. Значение в формате <a href="https://www.ietf.org/rfc/rfc3339.txt">RFC3339</a>.</p> <p>Строка в формате <a href="https://www.ietf.org/rfc/rfc3339.txt">RFC3339</a>.</p> 
done | **boolean** (boolean)<br><p>Если значение равно ``false`` — операция еще выполняется. Если ``true`` — операция завершена, и задано значение одного из полей ``error`` или ``response``.</p> 
metadata | **object**<br><p>Метаданные операции. Обычно в поле содержится идентификатор ресурса, над которым выполняется операция. Если метод возвращает ресурс Operation, в описании метода приведена структура соответствующего ему поля ``metadata``.</p> 
error | **object**<br>Описание ошибки в случае сбоя или отмены операции. <br> включает только одно из полей `error`, `response`<br><br><p>Описание ошибки в случае сбоя или отмены операции.</p> 
error.<br>code | **integer** (int32)<br><p>Код ошибки. Значение из списка <a href="https://github.com/googleapis/googleapis/blob/master/google/rpc/code.proto">google.rpc.Code</a>.</p> 
error.<br>message | **string**<br><p>Текст ошибки.</p> 
error.<br>details[] | **object**<br><p>Список сообщений с подробными сведениями об ошибке.</p> 
response | **object** <br> включает только одно из полей `error`, `response`<br><br><p>Результат операции в случае успешного завершения. Если исходный метод не возвращает никаких данных при успешном завершении, например метод Delete, поле содержит объект <a href="https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#empty">google.protobuf.Empty</a>. Если исходный метод — это стандартный метод Create / Update, поле содержит целевой ресурс операции. Если метод возвращает ресурс Operation, в описании метода приведена структура соответствующего ему поля ``response``.</p> 