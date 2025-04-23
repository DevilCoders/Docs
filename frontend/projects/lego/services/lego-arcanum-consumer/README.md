# Lego Client Adapter for Arcanum

Обеспечивает интеграцию с [Arcanum](https://wiki.yandex-team.ru/arcanum/).

## events

Адаптер слушает события `commentsToReviewPublished` из Арканума в [Logbroker](https://logbroker.yandex-team.ru/docs/).
[Lego Consumer](https://logbroker.yandex-team.ru/lbkx/accounts/lego?page=browser&type=account&sortOrder=%22default%22).

## env

* `LOGBROKER_CLIENT_ID` – название читателя, от имени которого будет осуществляться чтение.
* `LOGBROKER_TOKEN` – токен для подключения к Logbroker.
