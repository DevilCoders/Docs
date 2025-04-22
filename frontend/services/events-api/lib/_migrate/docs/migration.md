# Миграция данных со старой админки

1. Создать файл .env (пример лежит в .env.default)
2. Выполнить скрипты для импорта событий и для обновления города проведения (выполнять нужно на qloud-машинках):

```bash
npm run migrate:import-events
npm run migrate:update-events
```

3. В самом конце нужно не забыть установить sequence-ы на новое значение, в ином случае при попытке создать сущность,
база будет возвращать ошибку валидации, что запись с таким ID уже существует:

```
BEGIN;
LOCK TABLE events IN EXCLUSIVE MODE;
SELECT setval('events_id_seq', COALESCE((SELECT MAX(id)+1 FROM events), 1), false);
COMMIT;
```
