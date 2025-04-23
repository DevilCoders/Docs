# frontend-gh-app

Github App [VertisFrontendRobot](https://github.com/organizations/YandexClassifieds/settings/apps/vertisfrontendrobot)
Слушает разные события в репозиториях и делает соответствующие экшены
## Разработка

```sh
# Install dependencies
npm install

# Fetch secrets
npm run secrets

# Run the bot
npm start
```

## Тестирование
Есть тестовый апп, в нем установлен [тестовый апп](https://github.com/organizations/YandexClassifieds/settings/apps/vertisfrontendrobottest), Webhook URL которого настроен на локальный прокси smee.io, можно использовать его для локальных проверок.

Если локально не очень удобно или есть сомнение, как оно заработает в тестовом/продовом окружении - можно зайти на тестовый апп, в настройках подменить Webhook URL на урл балансера этого аппа и проверить полноценно интеграцию перед выкаткой. Важно не забыть, что Permission у аппов надо настроить и там и там, после этого не забыть апрувнуть изменения пермишнов в репозиториях

Тестинговое и дев-окружение смотрят на тестового-телеграм бота @TestVertisFrontendBot, можно спокойно его использовать для экспериментов, сильно спамить никому не будет

## Деплой 

```sh
make build
``` 

Далее через бота @vertis_shiva_bot 

```
/run -l test -v <short_hash> frontend-gh-app
```

С дальнейшим PROMOTE в продакшен

## Смена секретов
* `WEBHOOK_SECRET` - `ruby -rsecurerandom -e 'puts SecureRandom.hex(20)'` - полученное значение загрузить в [настройки аппа](https://github.com/organizations/YandexClassifieds/settings/apps/vertisfrontendrobot), выпустить новую версию в yav.yandex-team.ru
* `PRIVATE_KEY` - сгенерить ключ в [настройках аппа](https://github.com/organizations/YandexClassifieds/settings/apps/vertisfrontendrobot), полученный файл надо заискейпить (заменить line-breaks на `\n`), обрамить в кавычки `"<private_key>"`, выпустить новую версию в yav.yandex-team.ru
* `STARTREK_API_TOKEN` - сгенерировать токен для доступа к API Стартрека от нужного робота, загрузить новую версию в yav.yandex-team.ru
