## Смена статуса договора

Ручка позволяет изменять статус договора в [административном интерфейсе](https://arenda.test.vertis.yandex.ru/management/manager/flat/9ad36d78857947ffb6055d8eed4fa6e8/status/) сайта. Здесь [тестовый Swagger](http://realty-gateway-api.vrts-slb.test.vertis.yandex.net/index.html?url=/api/2.x/#!/rent32moderation/updateContractStatus).

### DRAFT
Возможно изменение из `Signing`, `SignedByOwner`, `Signed`, иначе `DRAFT_WRONG_STATUS_ERROR`.
Подробная информация [на странице](./signing-flow.html#draft).

### SEND_TO_OWNER
Возможно изменение только из `Draft`, иначе `SEND_TO_OWNER_WRONG_STATUS_ERROR`.
Подробная информация [на странице](./signing-flow.html#send-to-owner).

### SIGN_BY_OWNER
Возможно изменение только из `Signing`.
Подробная информация [на странице](./signing-flow.html#sign-by-owner).

### SIGN_BY_TENANT
Возможно изменение только из `Signed`.
Подробная информация [на странице](./signing-flow.html#sign-by-tenant).

### ACTIVATE
Возможно изменение из `Draft`, `Signed`, иначе `SET_ACTIVE_STATUS_ERROR`.
Подробная информация [на странице](./signing-flow.html#activate).
