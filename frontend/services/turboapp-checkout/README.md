# Турбо-приложение Формы Чекаута

Ссылки:

-   [Эпик на разработку](https://st.yandex-team.ru/TAP-1682)
-   [Графики балансера – тестинг](https://yasm.yandex-team.ru/template/panel/tap/upstream=checkout-testing-total/)
-   [Графики балансера – продакшн](https://yasm.yandex-team.ru/template/panel/tap/upstream=checkout-total/)

Окружения:

-   [Тестинг](https://checkout.tap-tst.yandex.ru/) (собирается автоматически из мастера)
-   [Релизный стенд](https://checkout.tap-rc.yandex.ru/) (собирается автоматически для релизной ветки)
-   [Продакшн](https://checkout.tap.yandex.ru/) (выкатывается релиз-инженером вручную)


## Запуск

Устанавливаем зависимости:

```bash
npx lerna bootstrap --scope @yandex-int/turboapp-checkout --include-filtered-dependencies
```

Для локальной разработки запускаем скрипт:

```bash
npx lerna run start --scope @yandex-int/turboapp-checkout --stream
```

Открыть приложение можно по ссылке [http://localhost:3000](http://localhost:3000).

Приложение автоматически перезапустится при изменениях в коде.
Ошибки линтинга можно увидеть в консоли.


## Команды

-   `npm start` – запуск приложения в режиме разработки
-   `npm run build` – сборка production версии приложения


## Разработка

-   [Подробнее про стор](./src/redux/README.md)
-   Документация по [React](https://reactjs.org)
-   Документация по [Create React App](https://facebook.github.io/create-react-app/docs/getting-started)


## Мониторинг ошибок

-   [Проект в Error Booster](https://error.yandex-team.ru/projects/turboapp-checkout/projectDashboard)
-   [Ошибки в проде за последний час](https://error.yandex-team.ru/projects/turboapp-checkout/projectDashboard?filter=environment%20==%20production&period=hour)
-   [Конфиг алертов](https://error.yandex-team.ru/projects/turboapp-checkout/settings/alerts)
-   [Настройки уведомлений](https://juggler.yandex-team.ru/notification_rules/?query=namespace%3DTAP)
