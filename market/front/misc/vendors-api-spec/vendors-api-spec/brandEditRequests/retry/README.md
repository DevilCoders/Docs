# Ресурс /brandEditRequests/retry

## GET /brandEditRequests/retry

Попытка повторно отправить в MBO все заявки в статусе "APPROVED"

### Доступы
  Ручка не предназначена для публичного доступа.

### Ответ
  <[SimpleResponse](/_entities/responses/SimpleResponse.md) [RetryResult] >

  `<RetryResult>`:
  - **retried** `<Integer>` - кол-во заявок, повторно отправленных в MBO
  - **successful** `<Integer>` - кол-во успешно отправленных заявок

### Примечания
  - Все успешно отправленные заявки переводятся в статус "CLOSED"
  - У всех заявок, для которых попытка отправки снова провалилась, обновляется значение поля `errorMessage`
