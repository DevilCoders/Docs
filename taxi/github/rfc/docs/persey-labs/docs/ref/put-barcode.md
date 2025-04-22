# Сохранить штрихкод заявки

Штрихкод заявки следует сохранять в Яндексе после того, как лаборатория подготовила [необходимый комплект документов](../concepts/workflow.md#prepare-documents).
 Яндекс свяжет номер, закодированный в штрихкоде, с номером заявки.

## Формат запроса

Чтобы сохранить штрихкод, отправьте PUT-запрос:

```http
PUT https://labs-api.yandex.ru/lab/v1/orders/barcode?id=<идентификатор заявки>

<тело запроса>
```

### Параметры запроса

| Query-параметр | Описание      |
| ------------- |--------------|
|  id  * | **Number**<br/> Идентификатор заявки, полученный от Яндекса. |

*Обязательный параметр.

### Тело запроса
```json
{
    "barcode": <штрихкод>  
}
```

| Параметр | Описание      |
| ------------- |--------------|
|  barcode  *  | **String**<br/> Данные штрихкода. |

*Обязательный параметр.

### HTTP-заголовки

В запросе необходимо передать заголовки:

```http
X-External-Service: <логин лаборатории>
X-External-Api-Key: <API-ключ>
Origin: https://labs-api.yandex.ru
```

Подробнее см. в разделе [Доступ к API](../concepts/authorization.md).

## Формат ответа

В случае успеха сервер возвращает статус 200 OK.

## Пример
```curl
curl -X PUT 'https://labs-api.yandex.ru/lab/v1/orders/status?id=400123456' \
 -H 'X-External-Service: msk_lab' \
 -H 'X-External-API-Key: Njrgku45vmklf34gffgft44saafvvvqqnrfmgl9h' \
 -H 'Origin: https://labs-api.yandex.ru' \
 -d '{ "barcode": "123-abc-123"}'
```