# Сервис регистрации событий для биллинга

https://wiki.yandex-team.ru/taxi/backend/hiring/architecture/corp-billing-events/

Как пользоваться:
1. Отправлять события из источников в `/v1/events`.
2. Узнавать об изменившихся топиках в `/v1/events/journal/topics`.
3. Получать объекты в `/v1/topics/compact`. Их можно использовать для
   формирования распоряжений в billing-orders.
4. А объекты в `/v1/topics/full` можно использовать для отображения в
   админке. Это самые настоящие обоснования распоряжений.

Лучше один раз увидеть!
```bash
# Запускаем сервис
make start-corp-billing-events

# В отдельной вкладке
bash services/corp-billing-events/usage-example.sh
```
