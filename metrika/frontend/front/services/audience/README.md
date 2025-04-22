1) Заводим виртуалку по инструкции:

https://wiki.yandex-team.ru/JandexMetrika/frontend/devcomputerforeveryone/

2) Затем на виртуалке:
```
cd ./services/audience

BUNDLE=audience LANGS=ru make compose-up
```

## Переменные окружения

Можно влиять на программу через переменные окружения, например собрать только русский язык:
```
LANGS=ru make compose-up
```

Другое окружение в bishop:
```bash
BISHOP_ENVIRONMENT_NAME=metrika.deploy.frontend.audience-bem.testing.development.rifler make compose-up
```

Все переменные окружения прокидываются в docker-compose.yml, откуда переменную можно прокинуть в нужный сервис
