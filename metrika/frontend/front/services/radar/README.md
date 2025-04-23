# Radar

1) Заводим виртуалку по инструкции:

https://wiki.yandex-team.ru/JandexMetrika/frontend/devcomputerforeveryone/

2) Ставим зависимости и запускаем:
```
cd ./frontend
npm run bootstrap:radar

cd ./services/radar

LANGS=ru make compose-up
```

## Переменные окружения

Можно влиять на программу через переменные окружения, например собрать только русский язык:
```
LANGS=ru make compose-up
```

Другое окружение в bishop:
```bash
BISHOP_ENVIRONMENT_NAME_BEM=metrika.deploy.frontend.radar-bem.testing.development.rifler make compose-up
```

Все переменные окружения прокидываются в docker-compose.yml, откуда переменную можно прокинуть в нужный сервис
