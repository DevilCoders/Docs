# @yandex-id/ipreg

Подробности тут https://wiki.yandex-team.ru/geotargeting/libgeobase/libipreg/?from=%2Flibgeobase%2Flibipreg%2F#libipreg1varkadii

Чистая nodejs реализация без бинарных биндингов

Файл со списком нужно взять тут: https://sandbox.yandex-team.ru/resources/?page=1&pageCapacity=20&type=IPREG_LAYOUT_STABLE&attrs=%7B%7D

Для автоматического получения свежей копии нужно

- либо в браузере открыть ссылку https://proxy.sandbox.yandex-team.ru/last/IPREG_LAYOUT_STABLE
- экспортировать переменную `SANDBOX_TOKEN` (взять тут https://oauth.yandex-team.ru/authorize?response_type=token&client_id=968e0e6d85d647feb327d893a42cf26f&optional_scope=sandbox:api) и использовать команду: `curl -o ipreg-base.json -H "Authorization: OAuth ${SANDBOX_TOKEN}" https://proxy.sandbox.yandex-team.ru/last/IPREG_LAYOUT_STABLE`

## Пример
```js
const ipregController = new IpregController('<путь к файлу с описанием сетей.json>');

return ipregController.isYandexAddr(user.ip);
```
