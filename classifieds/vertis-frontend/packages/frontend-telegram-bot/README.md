# `frontend-telegram-bot`

Приложение для работы с телеграм ботом VertisFrontendBot

Умеет обрабатывать http-запросы в апи для отсылки в чаты. При этом взаимодействие с серверами Telegram для получения команд ботика сделано через long-polling, чтобы не открывать приложение наружу

## Разработка

```sh
# Install dependencies
npm install

# Fetch secrets
npm run secrets

# Run the bot
npm start
```

## Деплой 

```sh
make build
``` 

Далее через бота @vertis_shiva_bot 

```
/run -l test -v <short_hash> frontend-telegram-bot
```

С дальнейшим PROMOTE в продакшен