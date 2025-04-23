# Ресурс /brandEditRequests/{id}

## GET /brandEditRequests/{id}

Получение заявки на редактирование бренда по идентификатору.

### Доступы
  - `vnd:moderation:read`

### Параметры
  - **uid** `<UID>` - обязательный параметр для аутентификации

### Ответ
  <[SimpleResponse](/_entities/responses/SimpleResponse.md) [[BrandEditRequest](/_entities/brand-editor/BrandEditRequest.md)] >

### Ошибки

#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)

#### Заявка не найдена
  - statusCode: `404`
  - code: `REQUEST_NOT_FOUND`
  - message: `No brand edit request found with ID: {id}`

## PUT /brandEditRequests/{id}

- Изменение заявки модератором (статусы полей, комментарии).
- Закрытие заявки

### Доступы
  - `vnd:moderation:write`

### Параметры
  - **uid** `<UID>` - обязательный параметр для аутентификации

### Данные
  - fieldsStatusData [`<Map[String, BrandFieldStatus]>`](/_entities/brand-editor/BrandFieldStatus.md) - статусы модерации заявки по отдельным полям
  - comment `<String>` - комментарий модератора
  - status `<String>` - статус заявки

  (См. описание [`<BrandEditRequest>`](/_entities/brand-editor/BrandEditRequest.md) для подробной информации по полям.)
  
### Ответ
  <[SimpleResponse](/_entities/responses/SimpleResponse.md) [[BrandEditRequest](/_entities/brand-editor/BrandEditRequest.md)] >
  
  Полная заявка с обновлёнными данными.
  
### Подробное описание работы

1. Модификация

Статусы полей и комментарий заявки являются "неизменными" (на самом деле нет) полями.
Каждый новый запрос полностью переписывает существующие данные. Т.е. если в запросе был передан
статус только для одного поля, значит заявка будет содержать статус только для этого одного поля,
независимо от того, были ли там какие-либо статусы до этого.

Такой способ модификации был признан наиболее прозрачным и удобным.

2. Закрытие

Если присланная заявка содержит статус "APPROVED" - запрос будет рассмотрен, как "закрывающий".
Закрыть можно только заявку у которой есть статусы для всех полей (не важно, положительные или нет),
а значит, закрывающий запрос должен содержать и статусы для всех полей (т.к. предыдущие будут переписаны),
и статус "APPROVED" для самой заявки.

В момент закрытия данные по всем полям **с положительным статусом** будут отправлены в MBO.
Если данные успешно отправлены - результирующая заявка будет иметь статус "CLOSED" и значение в поле `closedAt`.
Если попытка отправить данные провалилась - результирующая заявка будет иметь статус "APPROVED" и значение в поле `errorMessage`.

### Примечания
  - Значение поля `lastUpdatedAt` обновляется после каждого успешного вызова этой ручки
  - Единожды закрытую заявку уже нельзя модифицировать, значение поля `lastUpdatedAt` фактически становится датой закрытия.

### Ошибки

#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)

#### Заявка не найдена
  - statusCode: `404`
  - code: `REQUEST_NOT_FOUND`
  - message: `No brand edit request found with ID: {id}`

#### Попытка изменить заявку в нередактируемом статусе (см. [описание сущности](/_entities/brand-editor/BrandEditRequest.md))
  - statusCode: `400`
  - code: `NON_EDITABLE_STATUS`
  - message: `Cannot change request in status: {status}`

#### Присланная заявка содержит статусы для отсутствующих полей
  - statusCode: `400`
  - code: `ILLEGAL_FIELDS_FOUND`
  - message: `Specified fields aren't found in the request: {list of illegal fields}`

#### Попытка закрыть заявку без вынесения решения по всем полям
  - statusCode: `400`
  - code: `SOME_FIELDS_MISSING`
  - message: `Request cannot be closed without info for these fields: {list of missing fields}`
  
#### Заявка в запросе имеет статус `CLOSED`
  - статус-код: `400`
  - type: `BAD_PARAM`
  - message: `"Illegal request status: 'CLOSED'! Request may only be 'APPROVED'!"`

#### Присланный комментарий имеет слишком большую длину
  - statusCode: `400`
  - code: `BAD_PARAM`
  - message: `Illegal '${field}' length: ${length}! Maximum is: ${max_length}`
  
  Примеры сообщения:
  - `"Illegal 'comment' length: 784! Maximum is: 512"`
  - `"Illegal 'fieldsStatusData.name.comment' length: 784! Maximum is: 512"`

### Тестинг

В момент закрытия заявка может иметь специальный комментарий:
- `SYS:NO_COMMIT` - данные не будут отправлены в MBO вообще, но заявка попадёт в статус "CLOSED", как будто данные были успешно отправлены.
- `SYS:FAIL_COMMIT` или `SYS:FAIL_COMMIT:{n}` - отправка данных в MBO упадёт `{n}` раз со специальным сообщением
`"SYS:FAIL_COMMIT:{m}: for testing"`, где `{m}` номер текущего падения. Т.е. если закрыть заявку с комментарием
`"SYS:FAIL_COMMIT:2"`, то попытка коммита упадёт 2 раза с сообщениями:
`"SYS:FAIL_COMMIT:1: for testing"` и `"SYS:FAIL_COMMIT:2: for testing"`, а затем отработает по-настоящему.
 (`SYS:FAIL_COMMIT` равен `SYS:FAIL_COMMIT:1`).

## DELETE /brandEditRequests/{id}

Удаление заявки

### Доступы
  Ручка не предназначена для публичного доступа.

### Параметры
  - **uid** `<UID>` - обязательный параметр для аутентификации

### Ответ
  <[SimpleResponse](/_entities/responses/SimpleResponse.md) [[BrandEditRequest](/_entities/brand-editor/BrandEditRequest.md)] >
  
  Присланная заявка не имеет поля `id`.

### Ошибки

#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)

#### Заявка не найдена
  - statusCode: `404`
  - code: `REQUEST_NOT_FOUND`
  - message: `No brand edit request found with ID: {id}`

#### Попытка удалить заявку в статусе "CLOSED"
  - statusCode: `400`
  - code: `BAD_PARAM`
  - message: `Request is already CLOSED - you cannot delete it`
