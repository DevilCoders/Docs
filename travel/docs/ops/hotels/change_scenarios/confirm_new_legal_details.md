---
title: Подтвердить переход на новое юр. лицо у опубликованного отеля
---
## Подтвердить переход на новое юр. лицо у опубликованного отеля

Сначала нужно зарегистрировать новые юр. данные. Для этого нужно выполнить следующий скрипт, подставив айдишники **новых** юр. данных:
```sql
begin transaction;

update legal_details
set state = 1  -- new
where id = '<legal_details_id>';

INSERT INTO workflow_events(id, workflow_id, created_at, class_name, data, state)
VALUES (
   nextval('workflow_events_id_seq'),
   '<legal_details_workflow_id>',
   now(),
   'ru.yandex.travel.hotels.administrator.workflow.proto.TRegisterLegalDetails',
   decode('', 'base64'),
   1
);

end;
```

После этого нужно удостовериться, что Юр. данные зарегистрированы, после чего перевести отель в состояни `Published`:
```sql
begin transaction;

update hotel_connections
set state = 3  -- published
where id = '<hotel_connection_id>';

end;
```