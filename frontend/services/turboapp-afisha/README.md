# Турбо-приложение для Афиши

## Запуск

Настраиваем получение секретов для TVM:
- Получить OAuth токен для доступа к секретнице [по ссылке](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=ce68fbebc76c4ffda974049083729982)
- Скопировать полученный токен и подставить в команду вместо `OAUTH_TOKEN`
```bash
npm config set @yandex-int/turboapp-afisha:yav_token OAUTH_TOKEN
```

Устанавливаем зависимости:
```bash
npx lerna bootstrap --scope @yandex-int/turboapp-afisha --include-filtered-dependencies
```

Для локальной разработки запускаем скрипт:
```bash
npx lerna run start --scope @yandex-int/turboapp-afisha --stream
```

Открыть приложение можно по ссылке [http://localhost:3000](http://localhost:3000).

Приложение автоматически перезапустится при изменениях в коде.
Ошибки линтинга можно увидеть в консоли.

## Команды

- `npm start` – запуск приложения в режиме разработки
- `npm run build` – сборка production версии приложения
- `npm run update-api-stub` – обновление моков для API (требует запущенного рядом приложения)

## Замокать API

Чтобы обновить моки - в корне выполнить
```bash
SERVER_URL=http://localhost:8080/api npm run update-api-stub
```

## Разработка

- [Подробнее про стор](./src/app/redux/README.md)
- Документация по [Create React App](https://facebook.github.io/create-react-app/docs/getting-started/).
- Документация по [React](https://reactjs.org/).
