---
title: Отклонить изменения по полям юр. лица и обратно подключить отель.
---
## Отклонить изменения по полям юр. лица и обратно подключить отель.

**Применять только если ИНН, КПП, БИК и Р/С не поменялись!**  
Если мы отклоняем данные, пришедшие от Партнера, то чтобы обратно включить отель без обновления юр. данных, нужно выполнить следующий SQL скрипт:
```sql
begin transaction;

update hotel_connections
set state = 3   -- published
where id = '<ID_of_HotelConnection>';

update legal_details
set state = 3   -- registered
where id = '<ID_of_LegalDetails>';

-- skipping all updates - do not apply them to legal details
UPDATE legal_details_updates
SET state = 'skipped'
WHERE legal_details_id = '<ID_of_LegalDetails>' and state = 'pending';

end;
```