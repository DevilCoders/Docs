## Ресурс /vendors/{vendorId}/brandEditRequests/last

### GET /vendors/{vendorId}/brandEditRequests/last

Получение последней заявки, **созданной** определённым вендором.

### Доступы
  - `vnd:brand-content:read`

### Параметры
  - **uid** `<UID>` - обязательный параметр для аутентификации

### Ответ
  <[SimpleResponse](/_entities/responses/SimpleResponse.md) [[BrandEditRequest](/_entities/brand-editor/BrandEditRequest.md)] >

### Примечания
- **Эта ручка игнорирует заявки, созданные модератором** (поле `sourceRequestId` никогда не будет присутствовать)
- *Ручка предназначена для использования юзером вендора, так что она не отображает некоторые данные:*
  - Заявка присланная в ответ на эту ручку **не может иметь поле** `errorMessage`