# Резолвер addUserInterests

## Описание

Сохраняет интересы пользователя.
При повторном сохранении перезатирает данные.
Если отправить пустой массив - удалит интересы.

В ответе приходит статус сохранения: null или ошибка.

## Параметры

| Parameter | Type | Description | Default |
|---------------|----------|------------------|------------------|
| `interestIds` | array | Массив айдишников интересов | - |

Ссылочки:

- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/api/app/handlers/addUserInterests/v1/index.js)
- [Описание сущности `interest` в проекте](https://github.yandex-team.ru/market/marketfront/blob/master/market/src/entities/interest/index.js)
