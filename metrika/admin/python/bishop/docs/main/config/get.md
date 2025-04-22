### Получение конфига через API

Ручка для получения конфига: `/api/v2/config/{program_name}/{environment_name}`

- Тип запроса: `GET`

В теле ответа передаётся текст конфига, а в заголовке bishop-config-version будет находиться версия конфига.
В заголовке bishop-config-format будет находиться формат конфига.

Ручка для получения версии: `/api/v2/version/{program_name}/{environment_name}`

- Тип запроса: `HEAD`

В заголовке bishop-config-version будет находиться версия конфига.
