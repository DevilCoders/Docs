# Ресурс /brandEditRequests/{id}/revert

## POST /brandEditRequests/{id}/revert

Создание корректирующей заявки на редактирование бренда

### Доступы
  - `vnd:moderation:write`

### Параметры
  - **uid** `<UID>` - обязательный параметр для аутентификации

### Данные
  `<Array[String]>`
  
  Список имён полей бренда, которые необходимо скорректировать.

### Ответ
  <[SimpleResponse](/_entities/responses/SimpleResponse.md) [[BrandEditRequest](/_entities/brand-editor/BrandEditRequest.md)] >

  Новая заявка на редактирование бренда, в которой:
  - Поле `sourceRequestId` содержит номер исходной заявки
  - Бренды содержат только те поля, которые были переданы в запросе
  - Для каждого поля, отвергнутого в оригинальной заявке, новое значения бренда оставлено таким же
  - Для каждого поля, одобренного в оригинальной заявке, в качестве нового значения бренда взято старое значение из оригинальной заявки.

### Ошибки

#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)

#### Заявка не найдена
  - statusCode: `404`
  - code: `REQUEST_NOT_FOUND`
  - message: `No brand edit request found with ID: {id}`

#### Прислан пустой список полей
  - statusCode: `400`
  - code: `EMPTY_REQUEST`
  - message: `No fields specified for revert!`

#### Попытка скорректировать незакрытую заявку
  - statusCode: `400`
  - code: `NON_EDITABLE_STATUS`
  - message: `Request is NOT closed! Cannot revert!`

#### Присланы невалидные имена полей
  - statusCode: `400`
  - code: `ILLEGAL_FIELDS_FOUND`
  - message: `Illegal field names to revert: {listOfIllegalNames}! Available fields for selected request: {listOfAvailableNames}`

Невалидными считаются:
- Неизвестное поле (такого поля у бренда нет в принципе)
- Поле, которого не было в основной заявке
- Поле со статусом "одобрено", но без "старого" значения

### Пример запроса
```
POST /brandEditRequests/22/revert?uid=12345
["name", "picture"]
```

Требования:
1. Существует заявка с ID = 22
2. Заявка 22 находится в статусе "CLOSED"
3. У заявки 22 присутствуют поля "name" и "picture"
4. Поля "name" и "picture" были отвергнуты, или в заявке для них присутствует "старое" значение