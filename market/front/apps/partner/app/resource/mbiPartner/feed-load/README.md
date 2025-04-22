# Методы загрузки фидов

* [getOauthToken] - Выводит oauth-токен, нужный для загрузки фида из Excel;
* [setOauthToken] - Сохраняет oauth-токен, нужный для загрузки фида из Excel;
* [getFeeds] - Получить список фидов магазина
* [getFeed] - Получение информации о фиде по id
* [createFeed] - Создать фид у магазина (фид должен быть провалидирован)
* downloadFileFeed - Получить файл загруженного фида
* [deleteFeed] - Удалить фид у магазина
* [uploadFeed] - Загрузить фид для валидации
* [validateFeed] - Запустить валидацию фида
* [feedValidationStatus] - Статус валидации фида с логом
* [editFeed] - Редактировать существующий фид у магазина
* [loadValidationReport] - Скачать результат валидации фида с csv
* [feedLog] - Возвращает информацию об индексировании для фида и лог фидпарсера.

[Как работает валидация фидов](https://wiki.yandex-team.ru/mbi/newdesign/components/market-payment/feed-validator/)

[getOauthToken]: https://wiki.yandex-team.ru/MBI/NewDesign/components/market-payment/token/
[setOauthToken]: https://wiki.yandex-team.ru/MBI/NewDesign/components/market-payment/token/
[getFeeds]: https://wiki.yandex-team.ru/MBI/NewDesign/components/market-payment/getFeeds/
[getFeed]: https://wiki.yandex-team.ru/MBI/NewDesign/components/market-payment/getFeed/
[createFeed]: https://wiki.yandex-team.ru/MBI/NewDesign/components/market-payment/post-feed-v2/
[editFeed]: https://wiki.yandex-team.ru/MBI/NewDesign/components/market-payment/put-feed-v2/
[deleteFeed]: https://wiki.yandex-team.ru/MBI/NewDesign/components/market-payment/feed/
[uploadFeed]: https://wiki.yandex-team.ru/MBI/NewDesign/components/market-payment/uploadFeed/
[validateFeed]: https://wiki.yandex-team.ru/MBI/NewDesign/components/market-payment/post-feed-v2-validate/
[feedValidationStatus]: https://wiki.yandex-team.ru/MBI/NewDesign/components/market-payment/post-feed-v2-validationParsed/
[feedLog]: https://wiki.yandex-team.ru/MBI/NewDesign/components/market-payment/feedLog/
