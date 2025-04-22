Все запросы в API маркируются с помощью `X-Crypta-Request-ID`.

Получить `X-Crypta-Request-ID` можно в заголовке ответа. Компоненты front-end должны предоставлять идентификатор запроса в случае ошибки.

Для того, чтобы найти [в логах](https://platform.yandex-team.ru/projects/crypta/api/production?tab=logs-beta&query=&tz=-180) информацию про конкретный запрос нужно использовать query вида
```
#@fields.X-Crypta-Request-ID:"request-884ab709-6ef4-4fb7-b1a1-868aa207b9ab"
```
