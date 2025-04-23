# Бэкенд для турбоаппов

- [Нагрузочное тестирование](docs/SHOOTING.md)

## Запуск

Устанавливаем зависимости:
```bash
npx lerna bootstrap --scope @yandex-int/tap-backend --include-filtered-dependencies
```

Для локальной разработки запускаем скрипт:
```bash
npx lerna run start --scope @yandex-int/tap-backend --stream
```

Открыть приложение можно через туннелер, ссылка формата `https://<username>-<project_id>-<inst_name>.ldev.yandex.ru` видна в консоли при запуске.

Приложение автоматически перезапустится при изменениях в коде.

## Доступные команды:

- `npm start` - Запустить приложение для локальной разработки
- `npm test` - Запустить тесты
- `npm run build` - Скомпилировать TypeScript
- `npm run tools:prettier` - Запустить prettier

## Мониторинг ошибок

-   [Проект в Error Booster](https://error.yandex-team.ru/projects/tap-backend/projectDashboard)
-   [Ошибки в проде за последний час](https://error.yandex-team.ru/projects/tap-backend/projectDashboard?filter=environment%20==%20production&period=hour)
-   [Конфиг алертов](https://error.yandex-team.ru/projects/tap-backend/settings/alerts)
-   [Настройки уведомлений](https://juggler.yandex-team.ru/notification_rules/?query=namespace%3DTAP)


## Сервис адресов. Полезные ссылки:

- https://github.yandex-team.ru/market-java/pers-address - Исходники
- http://pers-address.tst.vs.market.yandex.net/swagger-ui.html - Swagger API

## Сервис геокодирования. Полезные ссылки:

- https://a.yandex-team.ru/arc/trunk/arcadia/extsearch/geo - Исходники
- https://a.yandex-team.ru/arc/trunk/arcadia/extsearch/geo/GUIDE.md - Рекомендации
