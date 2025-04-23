## Quick start
**Note.** You have to setup environment variables MAPS_TELEGRAM_BOT_NAME, MAPS_TELEGRAM_BOT_TELEGRAM_TOKEN. You can find them in YAV.

#### Install [mongodb](https://www.mongodb.com/)
```
brew install mongodb
```

```
sudo mkdir -p /data/db
sudo chmod -R 0777 /data/

docker-compose up
```

After that, for developing, you should use @YandexMapsDevBot

## Project structure
```
.tanker/                Tanker settings
configs/                Configs
    secure/             Configs from telegram-bot-secure (tokens)
    translations/       Translations fetched from tanker
debian/                 Debianize scripts and configs
src/                    Sources
    api/                Wrappers for mongo and external services
    commands/           Bot commands
    lib/                Helpers
    middlewares/        Express-like middlewares
    scheduler/          Sheduler for async notifications
        commands/       Supported async commands
```

## [Architecture](docs/ARCHITECTURE.md)

## Docs
[Wiki](https://wiki.yandex-team.ru/maps/dev/ui/products/telegram-bot/)

## Run tests and vaildation
### Run static code checkers
```
npm run lint
```
