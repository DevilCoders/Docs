---
title: Подключить новый отель с подтверждением изменения реквизитов
---
## Подключить новый отель с подтверждением изменения реквизитов

В этой ситуации нужно сделать следующее:

1. Обратно опубликовать юр. данные и применить изменения к ним:
```sql
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
```

2. Отель перевести в состояние publishing и рестартануть процесс его подключения:
```sql
UPDATE hotel_connections
SET state = 2
WHERE id = '<hotel_connection_id>';

-- restart process of hotel publishing
INSERT INTO workflow_events(id, workflow_id, created_at, class_name, data, state)
VALUES (nextval('workflow_events_id_seq'),
        '<workflow_id_of_hotelConnection>',
        now(),
        'ru.yandex.travel.hotels.administrator.workflow.proto.TPublishingStart',
        decode('', 'base64'),
        1);
```