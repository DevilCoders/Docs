# Формат URI

## Новый формат URI велосипедных маршрутов

Префикс: `ymapsbm1://route/bicycle/v1?`

Параметры:

- `uri`:
    - имеет формат `<точка>~<протобуф>~<точка>~<протобуф>~...~<точка>`, где:
        - `<точка>` - точка из запроса (или ближайшая точка входа в объект) в формате `<x>,<y>`.
        - `<протобуф>` - [протобуф](https://a.yandex-team.ru/arc/trunk/arcadia/maps/bicycle/router/lib/uri.proto) в формате base64. В протобуфе указаны промежуточные точки маршрута.
    - всегда начинается и заканчивается точками из запроса.

Пример (реальная длина протобуфа может отличаться):
```
"ymapsbm1://route/bicycle/v1?65.574339,57.135291~CqIBCgoIoMK-NhC41sQ-EgUITxD4BBIFCGQQ3AcSBgiTCxDOFhIGCP0FEPgIEgYI8QUQ_AwSBgjPDhCgGxIGCPEDELoGEgYIkwkQtQsSBgjdFBDXJBIGCI8bEPMwEgYI-wYQhxQSBgj9HhDzKRIGCM0IEIUVEgYIvxsQkhQSBgjpGhCdIhIGCK8UEJUzEgYIzA4QxSESBgiMCBDjHBIGCJEIEJQG~65.560823,57.121956"
```
