## Инструмент анализирует "медленные" задачи и отправляет статистику в slack

### Переменные окружения
 - `SLACK_CHANNEL_ID` - required
 - `TIME_LIMIT_IN_MINS` - default=30
 - `DATE_FROM_IN_HOURS` - default=24

### Запуск
```sh
npm i @yandex-int/frontend-speed-analizer
SLACK_CHANNEL_ID=<ID> npx @yandex-int/frontend-speed-analizer
```

### Деплой

Дождаться релиза новой версии.
Открыть [шедулер](https://sandbox.yandex-team.ru/scheduler/43207/view).
Поменять в конфиге версию пакета, см. в конфиге команду:
```sh
npm i @yandex-int/frontend-speed-analyzer@0.0.6 --registry=http://npm.yandex-team.ru"
```
