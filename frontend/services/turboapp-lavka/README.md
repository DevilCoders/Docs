# Турбо-приложение для Лавки

Ссылки:

- [Документация по API](https://st.yandex-team.ru/TAP-1177/)
- [Графики балансера – тестинг](https://yasm.yandex-team.ru/template/panel/tap/upstream=lavka-testing-total/)
- [Графики балансера – продакшн](https://yasm.yandex-team.ru/template/panel/tap/upstream=lavka-total/)

Окружения:

- [Тестинг](https://lavka.tap-tst.yandex.ru/) (собирается автоматически из мастера)
- [Релизный стенд](https://lavka.tap-rc.yandex.ru/) (собирается автоматически для релизной ветки)
- [Продакшн](https://lavka.tap.yandex.ru/) (выкатывается релиз-инженером вручную)

## Запуск

Устанавливаем зависимости:

```bash
npx lerna bootstrap --scope @yandex-int/turboapp-lavka --include-filtered-dependencies
```

Для локальной разработки запускаем скрипт:

```bash
npx lerna run start --scope @yandex-int/turboapp-lavka --stream
```

Открыть приложение можно через туннелер, ссылка формата `https://<username>-<project_id>-<inst_name>.ldev.yandex.ru` видна в консоли при запуске.

Для работы авторизации и других запросов в десктопном браузере необходимо добавить подстроку `SA/1.x TA/1.x` в `User agent`.

Приложение автоматически перезапустится при изменениях в коде.
Ошибки линтинга можно увидеть в консоли.

## Команды

-   `npm start` – запуск приложения в режиме разработки
-   `npm run build` – сборка production версии приложения

## API

АПИ Лавки доступно по двум путям:
- https://ya-authproxy.taxi.yandex.net/lavka - Продовое окружение.
- https://ya-authproxy.taxi.tst.yandex.net/lavka - Тестовое окружение.

Для наших продовых хостов ([lavka.tap.yandex.ru](https://lavka.tap.yandex.ru) и [lavka.tap-rc.yandex.ru](https://lavka.tap-rc.yandex.ru)) мы осуществляем походы в продовое окружение АПИ Лавки. Во всех остальных случаях пользуемся тестовым окружением АПИ.

Документация по API:
- [products](https://github.yandex-team.ru/taxi/uservices/blob/develop/services/overlord-catalog/docs/yaml/api/lavka_products.yaml)
- [suggest](https://github.yandex-team.ru/taxi/uservices/blob/develop/services/overlord-catalog/docs/yaml/api/suggest.yaml)
- [cart](https://github.yandex-team.ru/taxi/uservices/tree/develop/services/grocery-cart/docs/yaml)
- [orders](https://github.yandex-team.ru/taxi/uservices/tree/develop/services/grocery-orders/docs/yaml)

## Тестирование

Авторизация происходит по паспортным кукам. Чтобы её пройти нужно авторизоваться в Паспорте:
- https://passport.yandex.ru - Продовый Паспорт
- https://passport-test.yandex.ru - Тестовый Паспорт

Через [тестовую админку](https://testing-admin.eda.tst.yandex.net) можно управлять состоянием заказов. [Данные для входа](https://yav.yandex-team.ru/secret/sec-01er00g00n94v0p4trvn6bvjc4)

Релизные стенды доступны по двум путям:
- https://lavka.tap-rc.yandex.ru - Продовое АПИ Лавки.
- https://lavka-test.tap-rc.yandex.ru - Тестовое АПИ Лавки.

## Разработка

- [Подробнее про стор](./src/redux/README.md)
- Документация по [Create React App](https://facebook.github.io/create-react-app/docs/getting-started)
- Документация по [React](https://reactjs.org)


## Мониторинг ошибок

- [Проект в Error Booster](https://error.yandex-team.ru/projects/turboapp-lavka/projectDashboard)
- [Ошибки в проде за последний час](https://error.yandex-team.ru/projects/turboapp-lavka/projectDashboard?filter=environment%20==%20production&period=hour)
- [Конфиг алертов](https://error.yandex-team.ru/projects/turboapp-lavka/settings/alerts)
- [Настройки уведомлений](https://juggler.yandex-team.ru/notification_rules/?query=namespace%3DTAP)
