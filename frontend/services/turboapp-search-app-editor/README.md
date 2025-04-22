# TurboApp редактора приложений в ПП

## Запуск

Устанавливаем зависимости:
```bash
npx lerna bootstrap --scope @yandex-int/turboapp-search-app-editor --include-filtered-dependencies
```

Для локальной разработки запускаем скрипт:
```bash
npx lerna run start --scope @yandex-int/turboapp-search-app-editor --stream
```

## Окружения

- [Production](https://search-app-editor.tap.yandex.ru/)
- [Релизный стенд](https://search-app-editor.tap-rc.yandex.ru/)
- [Тестинг](https://search-app-editor.tap-tst.yandex.ru/)

## Мониторинг ошибок

-   [Проект в Error Booster](https://error.yandex-team.ru/projects/turboapp-search-app-editor/projectDashboard)
-   [Ошибки в проде за последний час](https://error.yandex-team.ru/projects/turboapp-search-app-editor/projectDashboard?filter=environment%20==%20production&period=hour)
-   [Конфиг алертов](https://error.yandex-team.ru/projects/turboapp-search-app-editor/settings/alerts)
-   [Настройки уведомлений](https://juggler.yandex-team.ru/notification_rules/?query=namespace%3DTAP)
