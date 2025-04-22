# Резолвер resolveProductFactorsByCategory

## Описание

Возвращает заказы пользователя по идентификаторам


## Параметры

- orderIds: Идентификаторы заказов
- identifyUserBy: необязательный параметр, значения: ["uid",  "muid"], по умолчанию "uid"
- withChangeRequest
- withCashbackEmitInfo
- withArchived
- archived
- rgb
- status: Фильтр по статусу чека. К примеру: "NEW", "PRINTED".
- digitalEnabled: // Включает выдачу цифровых заказов
