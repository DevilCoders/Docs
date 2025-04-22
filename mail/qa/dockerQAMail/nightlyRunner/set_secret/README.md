# Описание

Модуль можно добавлять в свои питонячьи проекты сабмодулем и перед своими скриптами делать ```set_secrets()```
Все токены пропишутся в переменные окружения.
```
    os.environ["TESTPALM_API"]
    os.environ["STARTRECK_TOKEN"]
    os.environ["HITMAN_TOKEN"]
    os.environ["YT_TOKEN"]
    os.environ["YQL_TOKEN"]
    os.environ["STAT_TOKEN"]
```

Чтобы заработало, надо добавить свой токен секретницы в переменные окружения в VAULT_TOKEN при запуске скриптов локально и
токен поняшки при запуске скриптов на тачках.

Свой токен и токен поняшки можно взять по 
[урлу](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=ce68fbebc76c4ffda974049083729982)

![локально](https://jing.yandex-team.ru/files/a-zoshchuk/19-07-29_131306.png)
![в кулауде](https://jing.yandex-team.ru/files/a-zoshchuk/19-07-29_131815.png)
