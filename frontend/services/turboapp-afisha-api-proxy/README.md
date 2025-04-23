# Фронт-бэк прокси для доступа в API Афиши из Миниапа Афиши

Ссылки:
- [Документация по API](https://github.yandex-team.ru/Afisha/afisha-graphql/blob/master/docs/API.md)
- [Prod API](https://api.draqla.afisha.yandex.net/graphql)
- [Тестинг API](https://api.draqla.afisha.tst.yandex.net/graphql)
- [Тестинг API с продовыми данными](https://editor.api.draqla.afisha.tst.yandex.net/graphql)
- [GraphQL интерфейс](https://spring-admin.draqla.afisha.tst.yandex-team.ru/altair)

## Запуск

Настраиваем получение секретов для TVM:
- Получить OAuth токен для доступа к секретнице [по ссылке](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=ce68fbebc76c4ffda974049083729982)
- Скопировать полученный токен и подставить в команду вместо `OAUTH_TOKEN`
```bash
npm config set @yandex-int/turboapp-afisha-api-proxy:yav_token OAUTH_TOKEN
```

Устанавливаем зависимости:
```bash
npx lerna bootstrap --scope @yandex-int/turboapp-afisha-api-proxy --include-filtered-dependencies
```

Для локальной разработки запускаем скрипт:
```bash
npx lerna run start --scope @yandex-int/turboapp-afisha-api-proxy --stream
```

API становиться доступна по локальному адресу [http://localhost:8080](http://localhost:8080)
и через тунелер [https://username-2-ekb.ldev.yandex.ru](https://username-2-ekb.ldev.yandex.ru)

Приложение автоматически перезапустится при изменениях в коде.
Ошибки линтинга можно увидеть в консоли.

## Команды

- `npm start` – запуск приложения в режиме разработки
- `npm run build` – сборка production версии приложения
