# Турбо-приложение для Идеального интернет-магазина

Ссылки:

-   [Документация по API](https://wiki.yandex-team.ru/edadeal/projects-documentations/API-BookALook/)
-   [Графики балансера – тестинг](https://yasm.yandex-team.ru/template/panel/tap/upstream=ecom-testing-total/)
-   [Графики балансера – продакшн](https://yasm.yandex-team.ru/template/panel/tap/upstream=ecom-total/)

Окружения:

-   [Тестинг](https://ecom.tap-tst.yandex.net/) (собирается автоматически из мастера)
-   [Релизный стенд](https://ecom.tap-rc.yandex.net/) (собирается автоматически для релизной ветки)
-   [Продакшн](https://ecom.tap.yandex.net/) (выкатывается релиз-инженером вручную)

## Запуск

Устанавливаем зависимости:

```bash
npx lerna bootstrap --scope @yandex-int/turboapp-ecom --include-filtered-dependencies
```

Для локальной разработки запускаем скрипт:

```bash
npx lerna run start --scope @yandex-int/turboapp-ecom --stream
```

Открыть приложение можно по ссылке [http://localhost:3000](http://localhost:3000).

Приложение автоматически перезапустится при изменениях в коде.
Ошибки линтинга можно увидеть в консоли.

## Команды

-   `npm start` – запуск приложения в режиме разработки
-   `npm run build` – сборка production версии приложения

## Разработка

-   [Подробнее про стор](./src/redux/README.md)
-   Документация по [Create React App](https://facebook.github.io/create-react-app/docs/getting-started/).
-   Документация по [React](https://reactjs.org/).
