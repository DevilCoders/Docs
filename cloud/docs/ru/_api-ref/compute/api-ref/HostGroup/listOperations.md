---
editable: false
---

# Метод listOperations
Возвращает список операций указанной группы выделенных хостов.
 

 
## HTTP-запрос {#https-request}
```
GET https://compute.api.cloud.yandex.net/compute/v1/hostGroups/{hostGroupId}/operations
```
 
## Path-параметры {#path_params}
 
Параметр | Описание
--- | ---
hostGroupId | Обязательное поле. Идентификатор группы выделенных хостов для которой запрашивается список операций. Чтобы получить идентификатор группы выделенных хостов, используйте запрос [list](/docs/compute/api-ref/HostGroup/list).  Максимальная длина строки в символах — 50.
 
## Query-параметры {#query_params}
 
Параметр | Описание
--- | ---
pageSize | Максимальное количество результатов на странице ответа на запрос. Если количество результатов больше чем [pageSize](/docs/compute/api-ref/HostGroup/listOperations#query_params), сервис вернет значение [nextPageToken](/docs/compute/api-ref/HostGroup/listOperations#responses), которое можно использовать для получения следующей страницы.  Максимальное значение — 1000.
pageToken | Токен страницы. Установите значение [pageToken](/docs/compute/api-ref/HostGroup/listOperations#query_params) равным значению поля [nextPageToken](/docs/compute/api-ref/HostGroup/listOperations#responses) предыдущего запроса, чтобы получить следующую страницу результатов.  Максимальная длина строки в символах — 100.
 
## Ответ {#responses}
**HTTP Code: 200 - OK**

```json 
{
  "operations": [
    {
      "id": "string",
      "description": "string",
      "createdAt": "string",
      "createdBy": "string",
      "modifiedAt": "string",
      "done": true,
      "metadata": "object",

      // `operations[]` включает только одно из полей `error`, `response`
      "error": {
        "code": "integer",
        "message": "string",
        "details": [
          "object"
        ]
      },
      "response": "object",
      // конец списка возможных полей`operations[]`

    }
  ],
  "nextPageToken": "string"
}
```

 
Поле | Описание
--- | ---
operations[] | **object**<br><p>Ресурс Operation. Дополнительные сведения см. в разделе <a href="/docs/api-design-guide/concepts/operation">Объект Operation</a>.</p> 
operations[].<br>id | **string**<br><p>Идентификатор операции.</p> 
operations[].<br>description | **string**<br><p>Описание операции. Длина описания должна быть от 0 до 256 символов.</p> 
operations[].<br>createdAt | **string** (date-time)<br><p>Время создания ресурса в формате в <a href="https://www.ietf.org/rfc/rfc3339.txt">RFC3339</a>.</p> <p>Строка в формате <a href="https://www.ietf.org/rfc/rfc3339.txt">RFC3339</a>.</p> 
operations[].<br>createdBy | **string**<br><p>Идентификатор пользователя или сервисного аккаунта, инициировавшего операцию.</p> 
operations[].<br>modifiedAt | **string** (date-time)<br><p>Время, когда ресурс Operation последний раз обновлялся. Значение в формате <a href="https://www.ietf.org/rfc/rfc3339.txt">RFC3339</a>.</p> <p>Строка в формате <a href="https://www.ietf.org/rfc/rfc3339.txt">RFC3339</a>.</p> 
operations[].<br>done | **boolean** (boolean)<br><p>Если значение равно ``false`` — операция еще выполняется. Если ``true`` — операция завершена, и задано значение одного из полей ``error`` или ``response``.</p> 
operations[].<br>metadata | **object**<br><p>Метаданные операции. Обычно в поле содержится идентификатор ресурса, над которым выполняется операция. Если метод возвращает ресурс Operation, в описании метода приведена структура соответствующего ему поля ``metadata``.</p> 
operations[].<br>error | **object**<br>Описание ошибки в случае сбоя или отмены операции. <br>`operations[]` включает только одно из полей `error`, `response`<br><br><p>Описание ошибки в случае сбоя или отмены операции.</p> 
operations[].<br>error.<br>code | **integer** (int32)<br><p>Код ошибки. Значение из списка <a href="https://github.com/googleapis/googleapis/blob/master/google/rpc/code.proto">google.rpc.Code</a>.</p> 
operations[].<br>error.<br>message | **string**<br><p>Текст ошибки.</p> 
operations[].<br>error.<br>details[] | **object**<br><p>Список сообщений с подробными сведениями об ошибке.</p> 
operations[].<br>response | **object** <br>`operations[]` включает только одно из полей `error`, `response`<br><br><p>Результат операции в случае успешного завершения. Если исходный метод не возвращает никаких данных при успешном завершении, например метод Delete, поле содержит объект <a href="https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#empty">google.protobuf.Empty</a>. Если исходный метод — это стандартный метод Create / Update, поле содержит целевой ресурс операции. Если метод возвращает ресурс Operation, в описании метода приведена структура соответствующего ему поля ``response``.</p> 
nextPageToken | **string**<br><p>Этот токен позволяет получить следующую страницу результатов для списка запросов. Если количество результатов больше чем <a href="/docs/compute/api-ref/HostGroup/listOperations#query_params">pageSize</a>, используйте <a href="/docs/compute/api-ref/HostGroup/listOperations#responses">nextPageToken</a> в качестве значения параметра <a href="/docs/compute/api-ref/HostGroup/listOperations#query_params">pageToken</a> в следующем запросе списка ресурсов. Каждая следующая страница будет иметь свой <a href="/docs/compute/api-ref/HostGroup/listOperations#responses">nextPageToken</a> для продолжения перебора страниц результатов.</p> 