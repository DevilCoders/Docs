В Ртхабе используется обычный cm на Баше.

Ссылки:
* Вьювер: [https://rthub-cm.n.yandex-team.ru/targets](https://rthub-cm.n.yandex-team.ru/targets)
* Сервис: [https://nanny.yandex-team.ru/ui/#/services/catalog/rthub_clustermaster](https://nanny.yandex-team.ru/ui/#/services/catalog/rthub_clustermaster)
* Сборочный таск: [https://sandbox.yandex-team.ru/task/1319185473](https://sandbox.yandex-team.ru/task/1319185473)
* Основной скрипт: [https://a.yandex-team.ru/arcadia/robot/rthub/scripts/cm.sh](https://a.yandex-team.ru/arcadia/robot/rthub/scripts/cm.sh)

В сервис приезжают полностью папки robot/rthub/conf (в ./configs), robot/rthub/scripts (в ./scripts) и бинарные ресурсы из sandbox-таска. Можно свободно добавлять новые цели. При добавлении новых ресурсов не забывайте помечать их IsDynamic, иначе при выкатках cm будет перезапускаться.

