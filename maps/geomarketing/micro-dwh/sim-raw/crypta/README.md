# Данные Крипты

Скрипты объединены в отдельную директорию, так как они однотипны -
одинаковые запросы, только обращаются к разным таблицам.
Изначально, все id-шники из Крипты забирались в одном скрипте: https://paste.yandex-team.ru/8818924.
Но он выполняется около 1,5 часа. Запуская запросы по отдельности, самый долгий
выполняется около 20 минут.

***Важно, необходимо проверять наличие доступов у робота, так как к данным Крипты
доступы могут протухать.***

### Особенности:
* На ***zero_layer*** формируем список всех puid-ов, которые нужны.
* В скриптах используется JOIN с таблицей пользователей из zero_layer, так как
забирать данные всех пользователей не очень хорошо, с точки зрения безопасности.
* В связи с пунктом выше, появилась необходимость добавить второй слой загрузки
данных, на котором забирается дополнительная инфа по загруженным id. Это исключение,
такие ситуации надо минимизировать.

### Полезные ссылки:
- Про данные: https://wiki.yandex-team.ru/crypta/matching/consumers/yt/matchingdesc/
- Про доступы: https://wiki.yandex-team.ru/crypta/matching/consumers/yt/matchingdesc/roli-dlja-matchinga-identifikatorov-na-yt/

