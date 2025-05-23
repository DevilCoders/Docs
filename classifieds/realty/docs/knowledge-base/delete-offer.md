# Ручное удаление зависшего оффера
Зависший оффер - это оффер в неконсистентном состоянии, который по факту удален пользователем (или из фида), но до сих пор присутствует хотя бы в какой-то части сервиса.

Шаги по удалениию такого оффера:
1) убедиться, что оффер действительно завис (для vos оффера - получить ответ ручки воза, для фидового - что его нет в фиде)
2) дернуть ручку удаления оффера отовсюду  [utils_delete_offer_from_everywhere](http://realty-vos-api-http.vrts-slb.test.vertis.yandex.net/swagger/#!/utils/utils_delete_offer_from_everywhere). Ручка работает следующим образом:
- пытается зашедулить удаление оффера в возе (проставляется статус у оффера). В случае успеха воз посылает оффер в унифаер, который его удаляет через какое-то время и оффер по цепочке удалется из других мест.
- если оффера уже нет в возе, то пытаемся зашедулить удаление оффера из унифаера. В случае успеха унифаер удаляет у себя в базе оффер и по цепочке оффер удалется из других мест.
- если и в возе и в унифаере оффера нет, то удаляем оффер из rt кассандры и поискового индекса
3) если пункт 2) сработал и оффер был удален, то все ок. Но в некоторых случаях оффер даже после этого может остаться где-то висеть, тогда можно или попытаться еще раз его удалить выполнив пункт 2) или удалить его из этого места дернув соответствующую ручку индексатора [deleteOffer](http://realty-indexer-api.vrts-slb.test.vertis.yandex.net/#!/deleteOffer)
4) если нужно удалить оффер из модерации и пункты 2) и 3) не помогли, то можно дернуть ручку удаления оффера из модерации [deleteModerationOffer](http://realty-indexer-api.vrts-slb.test.vertis.yandex.net/#!/deleteOffer/deleteModerationOffer). Это крайняя мера (потому что мы затираем оффер в модерации) на случай, когда оффера нет в возе и унифаере, но он остался в модерации.
