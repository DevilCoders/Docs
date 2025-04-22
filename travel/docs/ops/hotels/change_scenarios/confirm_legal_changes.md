---
title: Подтвердить Юр. данные, пришедшие от партнера
---
## Подтвердить Юр. данные, пришедшие от партнера

Если мы подтверждаем данные, пришедшие от Партнера. То, чтобы обратно включить отель и обновить сущность "Юр. данные", нужно выполнить следующий SQL скрипт:
```sql
begin transaction;

update hotel_connections
set state = 3   -- published
where id = '<ID_of_HotelConnection>';

update legal_details
set state = 3   -- registered
where id = '<ID_of_LegalDetails>';

INSERT INTO workflow_events(id, workflow_id, created_at, class_name, data, state)
VALUES (
   nextval('workflow_events_id_seq'),
   '<Workflow ID of Legal Details>',
   now(),
   'ru.yandex.travel.hotels.administrator.workflow.proto.TUpdateLegalDetails',
   decode('', 'base64'),
   1
);

end;
```