# Резолвер resolveMuid

## Описание

Работает в режиме авторизации. Вначале проверяется, не превысил ли пользователь лимит на кол-во авторизаций (защита от DDoS). Если все хорошо, то пользователю присваивается специальный фейковый user id, который обозначим как muid (market user id).

Параметров не принимает

## Пример успешного ответа

```
{
    "results": [
        {
            "handler": "resolveMuid",
            "result": {
                "cookie": "1152921504819334995:XXX",
                "muid": "1152921504819334995"
            }
        }
    ],
    "collections": {}
}
```

## Пример неуспешного ответа

```
{
    "results": [
        {
            "handler": "resolveMuid",
            "error": {
                "kind": "ResolverMuidCookieHitRateLimitError",
                "message": "Hit rate limit of 10 new muids per 1 minute"
            }
        }
    ],
    "collections": {}
}
```
Ссылочки:

- [Описание метода](https://wiki.yandex-team.ru/market/marketplace/Dev/checkouter/post/auth/)
