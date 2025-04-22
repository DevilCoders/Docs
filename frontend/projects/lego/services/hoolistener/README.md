# hoolistener
Это Express приложение, которое умеет обрабатывать разные запросы.
Сервис размещается в [`deploy`](https://deploy.yandex-team.ru/stages/lego_hoolistener_production).
Запускается из докера.

Используется командой Лего для работы с [/canary](./insideCanary.md) и [проверкой совместимости пакетов](./check.md).

## Список доступных ручек:
- [comment](./routes/comment.md)
- [push](./routes/push.md)
- [status](./routes/status.md)
- [pull-request](./routes/pull-request.md)

## Разработка
Инструкция для разработчика лежит в файле [dev.md](./dev.md)

## Поддержка
Поддержкой занимается команда Лего, со всеми вопросами стоит приходить в slack или в рассылку.
