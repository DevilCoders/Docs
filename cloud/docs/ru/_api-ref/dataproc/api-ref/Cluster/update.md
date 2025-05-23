---
editable: false
---

# Метод update
Обновляет конфигурацию указанного кластера.
 

 
## HTTP-запрос {#https-request}
```
PATCH https://dataproc.api.cloud.yandex.net/dataproc/v1/clusters/{clusterId}
```
 
## Path-параметры {#path_params}
 
Параметр | Описание
--- | ---
clusterId | Идентификатор кластера, который следует изменить.  Чтобы получить идентификатор кластера, выполните запрос [list](/docs/data-proc/api-ref/Cluster/list).  Максимальная длина строки в символах — 50.
 
## Параметры в теле запроса {#body_params}
 
```json 
{
  "updateMask": "string",
  "description": "string",
  "labels": "object",
  "configSpec": {
    "subclustersSpec": [
      {
        "id": "string",
        "name": "string",
        "resources": {
          "resourcePresetId": "string",
          "diskTypeId": "string",
          "diskSize": "string"
        },
        "hostsCount": "string"
      }
    ]
  },
  "name": "string",
  "serviceAccountId": "string",
  "bucket": "string"
}
```

 
Поле | Описание
--- | ---
updateMask | **string**<br><p>Маска поля, которая указывает, какие атрибуты кластера должны быть изменены.</p> <p>Имена всех обновляемых полей, разделенные запятыми. Только значения указанных полей будут изменены. Остальные останутся нетронутыми. Если поле указано в параметре ``updateMask`` и в запросе не было отправлено значение для этого поля, значение поля будет сброшено на значение по умолчанию. Значение по умолчанию для большинства полей — null или 0.</p> <p>Если в запросе не передается ``updateMask``, значения всех полей будут обновлены. Для полей, указанных в запросе, будут использованы переданные значения. Значения остальных полей будут сброшены на значения по умолчанию.</p> 
description | **string**<br><p>Новое описание кластера.</p> <p>Максимальная длина строки в символах — 256.</p> 
labels | **object**<br><p>Новый набор меток кластера в виде пар ``ключ: значение``.</p> <p>Не более 64 на ресурс. Длина строки в символах для каждого ключа должна быть от 1 до 63. Каждый ключ должен соответствовать регулярному выражению ``[a-z][-_0-9a-z]*``. Максимальная длина строки в символах для каждого значения — 63. Каждое значение должно соответствовать регулярному выражению ``[-_0-9a-z]*``.</p> 
configSpec | **object**<br><p>Конфигурация и ресурсы хостов, которые должны быть созданы для кластера Data Proc.</p> 
configSpec.<br>subclustersSpec[] | **object**<br><p>Новая конфигурация для подкластеров в кластере.</p> 
configSpec.<br>subclustersSpec[].<br>id | **string**<br><p>Идентификатор подкластера, который следует изменить.</p> <p>Чтобы получить идентификатор подкластера, используйте запрос <a href="/docs/data-proc/api-ref/Subcluster/list">list</a>.</p> 
configSpec.<br>subclustersSpec[].<br>name | **string**<br><p>Имя подкластера.</p> <p>Значение должно соответствовать регулярному выражению ``\|[a-z][-a-z0-9]{1,61}[a-z0-9]``.</p> 
configSpec.<br>subclustersSpec[].<br>resources | **object**<br><p>Конфигурация ресурсов для каждого хоста в подкластере.</p> 
configSpec.<br>subclustersSpec[].<br>resources.<br>resourcePresetId | **string**<br><p>Идентификатор набора вычислительных ресурсов, доступных хосту (процессор, память и т. д.). Все доступные наборы ресурсов перечислены в <a href="/docs/data-proc/concepts/instance-types">документации</a>.</p> 
configSpec.<br>subclustersSpec[].<br>resources.<br>diskTypeId | **string**<br><p>Тип хранилища для хоста. Возможные значения:</p> <ul> <li>network-hdd — сетевой HDD-диск;</li> <li>network-ssd — сетевой SSD-диск.</li> </ul> 
configSpec.<br>subclustersSpec[].<br>resources.<br>diskSize | **string** (int64)<br><p>Объем хранилища, доступного хосту, в байтах.</p> 
configSpec.<br>subclustersSpec[].<br>hostsCount | **string** (int64)<br><p>Количество хостов в подкластере.</p> <p>Минимальное значение — 1.</p> 
name | **string**<br><p>Новое имя кластера Data Proc. Имя должно быть уникальным в рамках каталога.</p> <p>Значение должно соответствовать регулярному выражению ``\|[a-z][-a-z0-9]{1,61}[a-z0-9]``.</p> 
serviceAccountId | **string**<br><p>Идентификатор сервисного аккаунта, которым должен пользоваться агент Data Proc для управления задачами.</p> 
bucket | **string**<br><p>Имя нового бакета Object Storage, который следует использовать для задач Data Proc.</p> 
 
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