## Build and run

```ya make && ./lunaparkapi --port 80```

Make sure that env variables are set properly.
The list of env variables can be found [here](settings.py).

## Quantiles data handler
The parameter ```job``` takes any job id from [Lunapark testing](https://lunapark-develop.in.yandex-team.ru/) database

```curl -i 'https://lunaparkapi-testing.in.yandex-team.ru/datalens?job=1822827' -H 'X-Ya-Service-Ticket: OAuthfdwg'```

TVM2 service tickets are supported.
LunaparkAPI TVM2 service id: [2025716](https://abc.yandex-team.ru/services/lunapark/resources/?show-resource=27059016)

The handler ```report``` gives the same result, but it doesn't need authorizaton:
```curl -i 'https://lunaparkapi-testing.in.yandex-team.ru/report?job=1822827```
This handler is used only for debug purposes and should be deleted after CI test task creation.
