# generator-market

Пакет для генерации базовых сущностей.

Сделан для [yeoman](https://yeoman.io/).

Вики: <https://wiki.yandex-team.ru/Market/frontend/tools/generator-market/>

[![Watch simple demo](https://jing.yandex-team.ru/files/prvlv/Снимок%20экрана%202020-10-04%20в%2017.50.27.png)](https://s101iva.storage.yandex.net/rjing/U2FsdGVkX19xQ1RwOUX-r37W3D6QieGkA6iYQmY7PU39VC3nJka_wutoxdchRvwdSwKqwXaa3KzajWlfhHdO9prsO7S7ZNii09c_ppkhXSU?ts=0005b0d990db4f53&content_type=video%2fmp4&filename=gm.mp4&disposition=inline&sign=9f044ab6d94a61ca16d25e62ad8042996a2a1889768b19e231326debfad83f95)

## Начало работы

1. Установить yeoman:
`npm install -g yo`
1. Установить этот пакет:
`npm install -g @yandex-market/generator-market`

## Обновление

`npm install -g @yandex-market/generator-market`

## Использование

Можно выполнить `yo @yandex-market/market` для просмотра списка доступных генераторов.

Генераторы запускаюся так:
`yo market:entity <название entity в camel case>`

генератор может попросить ответить на несколько вопросов, после чего создаст необходимые файлы и выдаст copy-paste код для использования сгенерированного.

### Доступные генераторы

Команда `yo @yandex-market/market` выведет доступные на данный момент возможности

### Базовая директория для результатов

По умолчанию результаты уже кладутся в директории, которые не надо указыать.

Но есть возможность этим управлять в генераторах component и widget.

Для этого достаточно указать путь через ` -- src/some/path`.

Примеры:

```
yo market:component myNewComponent -- src/uikit/components
yo market:component outletPreloader -- src/widgets/content/checkout/common/CheckoutDeliveryEditor/components
```

## Как внести изменения

- Прочитай [доку](https://yeoman.io/).  
- Внутри директории выполни `npm link @yandex-market/generator-market`.  
- Внеси правки.
- ...  
- Commit. Push. PR.