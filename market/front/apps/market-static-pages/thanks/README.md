# Страница "Спасибо"

Страница для отзывов: [market.yandex.ru/thanks](https://market.yandex.ru/thanks).
На неё редиректится пользователь при поиске по слову "спасибо".

## Глобальные зависимости

В системе должны быть установлены `node`, `npm`.

## Установка

1. Запустить команду `npm i`

## Сборка приложения

* `npm run dev` — запустить приложение в dev режиме
* `npm run build:prod` — запустить сборку prodiction версии приложения

Перед тем, как закомитить изменения, не забудьте проверить код с помощью линтера:

```sh
npm run lint
```

## Сборка приложения на сервере
* `npm i` — установка зависимостей
* `NODE_ENV=production npm run build:prod` — запуск сборки приложения

## Как освежить фотографии сотрудников?

1. Выкачайте и обрежьте фотографии сотрудников со Стаффа [с помощью скрипта](https://github.yandex-team.ru/quasiyoke/autothanks),
1. смените в коде константу `IMAGES_COUNT`, чтобы она соответствовала общему количеству получившихся картинок.
