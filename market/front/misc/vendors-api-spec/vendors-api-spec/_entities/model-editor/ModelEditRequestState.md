# Сущность "ModelEditRequestState"

Состояние заявки на создание/изменение модели с точки зрения пользователя.
Одно состояние может соответствовать нескольким статусам [`ModelEditRequestStatus`](ModelEditRequestStatus.md)

### Значения:
  - "PUBLISHED" - заявка опубликована. Соответствует статусу: COMPLETED
  - "EDITING" - заявка в редактировании или требует редактирования. Статусы: NEW, NEED_FIX, NEED_INFO
  - "PROCESSING" - заявка принята и находится в обработке. Статусы: ACCEPTED, PROCESSING
  - "REJECTED" - заявка отклонена. Статусы: REJECTED, REJECTED_DUPLICATED, REJECTED_UNKNOWN_BRAND, REJECTED_UNKNOWN_CATEGORY, REJECTED_UNKNOWN_MODEL
