# Фронтенд сервиса Виджет оферты такси

Виджет оферты такси

## Хосты

s
Статика деплоится в s3

-   testing - https://yastatic.net/s3/taxi-front/corp-client/widgets/testing/offer-form/bundle.js
-   stable - https://yastatic.net/s3/taxi-front/corp-client/widgets/production/offer-form/bundle.js

PS. У виджета unstable нет.

Проверять задеплоенное можно в проекте [КК](https://github.yandex-team.ru/taxi/frontend-monorepo/tree/master/services/corp-corp-client)

-   unstable - https://corp-client.taxi.dev.yandex.ru/pages/offer
-   testing - https://corp-client.taxi.tst.yandex.ru/pages/offer (то же самое что и в unstable)
-   stable - https://business.taxi.yandex.ru/pages/offer

## Установка и разработка

-   `cd services/corp-offer-form/`
-   `npm run install`
-   `npm start`

Откроется страница для разработки, через квери параметры можно менять конфигурацию виджета.
Доступны следующие параметры:

-   contractType
-   theme
-   locale
-   country

## Сборка

-   `npm run build:{ENV}` — ENV: stable | testing | unstable

## Локализация

Для локализации используется [tanker-kit](https://github.yandex-team.ru/search-interfaces/frontend/tree/f5b00cb03d009996a9744b81617123871d3a0b4f/packages/tanker-kit)

Проект в танкере: https://tanker-beta.yandex-team.ru/project/corp-offer-form

1. Получаем токен здесь https://nda.ya.ru/3SjQY7.
2. Кладем его в `./.tanker/secrets.js` вот так

```javascript
module.exports = {
    token: '...token',
};
```

3. Запускаем команду `npm run tanker:pull`.
4. После этого переводы будут обновлены локально в папке `./src/translations`

## Релиз

[Как собирать и катить релиз](https://wiki.yandex-team.ru/taxi/efficiency/dev/frontend/rtc/fast-create-service/#razrabotka)
