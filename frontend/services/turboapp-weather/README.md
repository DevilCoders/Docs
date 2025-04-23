# Турбо-приложение для Погоды

Ссылки:

-   [Документация по API](https://wiki.yandex-team.ru/weather/api/)
-   [Графики балансера – тестинг](https://yasm.yandex-team.ru/template/panel/tap/upstream=weather-testing-total/)
-   [Графики балансера – продакшн](https://yasm.yandex-team.ru/template/panel/tap/upstream=weather-total/)

Окружения:

-   [Тестинг](https://weather.tap-tst.yandex.ru/) (собирается автоматически из мастера)
-   [Релизный стенд](https://weather.tap-rc.yandex.ru/) (собирается автоматически для релизной ветки)
-   [Продакшн](https://weather.tap.yandex.ru/) (выкатывается релиз-инженером вручную)

## Запуск

Устанавливаем зависимости:

```bash
npx lerna bootstrap --scope @yandex-int/turboapp-weather --include-filtered-dependencies
```

Для локальной разработки запускаем скрипт:

```bash
npx lerna run start --scope @yandex-int/turboapp-weather --stream
```

Открыть приложение можно по ссылке https://<nickname>-1-ekb.ldev.yandex.ru/pogoda/.

Приложение автоматически перезапустится при изменениях в коде.
Ошибки линтинга можно увидеть в консоли.

## Команды

-   `npm start` – запуск приложения в режиме разработки
-   `npm run build` – сборка production версии приложения

## Моки

Позволяют вывести погодные алерты на главном экране под почасовым прогнозом

-   `?usemock=alerts-combo-1`
-   `?usemock=alerts-combo-2`
-   `?usemock=alerts-combo-3`

## Разработка

-   [Подробнее про стор](./src/redux/README.md)
-   Документация по [Create React App](https://facebook.github.io/create-react-app/docs/getting-started/).
-   Документация по [React](https://reactjs.org/).

## Мониторинг ошибок

-   [Проект в Error Booster](https://error.yandex-team.ru/projects/turboapp-weather/projectDashboard)
-   [Ошибки в проде за последний час](https://error.yandex-team.ru/projects/turboapp-weather/projectDashboard?filter=environment%20==%20production&period=hour)


## Локальный запуск скриншот-тестов

`npm run build` – потому что для тестов нужна продакшн-сборка
`npm start` – запустить приложение
`DEV={ваш логин} npm run hermione:gui` – запустить тесты (но все разом лучше не стоит, лучше ограничить файлом или с помощью grep)

## Локальный запуск unit-тестов

`npm run build` – потому что для тестов нужна продакшн-сборка
`npm run unit` или `npm run unit:ssr` – запустить тесты
