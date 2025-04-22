# Резолвер resolveBindByMuid

## Описание

Привязать монеты к залогину по muid.



## Пример успешного ответа

```
{
    "results": [
        {
            "handler": "resolveBindByMuid",
            "result": [
                123
            ],
        }
    ],
    "collections": {
        coin: {
            [123]: {
                id: 123,
                subtitle: 'test',
                type: 'FIXED',
                description: 'description test',
                images: {standart: ''},
                status: 'INACTIVE',
                reason: 'ORDER',
            }
        }
    }
}
```

## Привер не успешного ответа

```
{
    "results": [
        {
            "handler": "resolveBindByMuid",
            "error": {
                "kind": "ResolverMuidCookieHitRateLimitError",
                "message": "Hit rate limit of 10 new muids per 1 minute"
            }
        }
    ],
    "collections": {}
}
```

## возможные ошибки приходящие с бека: 

 - 403 (FORBIDDEN) если неверная кука muid, 
 - USER_IN_BLACKLIST если пользователь забанен, 
 - NOT_COIN_OWNER (часть монет уже была привязана другим пользоватлеям)


### Ссылочки:

- [Описание метода](http://market-loyalty.tst.vs.market.yandex.net:35815/swagger-ui.html@self/platform/coins-controller/bindCoinsToUserUsingPUT_1)