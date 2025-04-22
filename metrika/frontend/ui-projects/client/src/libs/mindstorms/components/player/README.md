# Компонент плеера

Данный компонент является оберткой над Яндексовым плеером команды видеохостинга
[ссылка на репозиторий плеера](https://a.yandex-team.ru/arcadia/player/web-player).

## Поддерживаемые форматы видео

Работает только с следующими форматами:

-   HLS
-   MPEG-dash

## Как пользоваться?

Команда видеохостинга дает пользоваться своим компонентом с помощью скрипта, встраиваемого на сайт. Напоминает схему
работы Яндекс.Карт или нашего кода счетчика.

1. Чтобы пользоваться нашим компонентом, необходимо в конкретный `index.html` нужного сервиса добавить:

    ` <script async src='https://frontend.vh.yandex.ru/stable/player_version/player.js'></script>`

    Они обычно лежат по пути `client/src/services/${SERVICE_NAME}/public/index.html`

2. Теперь можно встраивать компонент `<Player>`, он будет работать.

## Полезные ссылки

-   [Стенд плеера](https://playerweb-ci.s3.mds.yandex.net/video-player-iframe-api/stands/trunk/index.html)
-   [Публичное типы API движка плеера](https://a.yandex-team.ru/arcadia/player/web-player/packages/public-types)
-   [Документация на типы](https://playerweb-ci.s3.mds.yandex.net/video-player-iframe-api/stands/trunk/docs-v2/index.html)
