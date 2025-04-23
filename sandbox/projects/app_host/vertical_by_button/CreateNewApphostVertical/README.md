# CreateNewApphostVertical

## Общее описание
Данная задача (`CreateNewApphostVertical`) является входной точкой для запуска создания вертикали Apphost'a.
Она проверяет, что у сервиса, для которого создается вертикаль, есть все необходимые доступы, в т.ч.:
* Существует abc-группа с id или slug, который указан в соотв. input-поле задачи
* Робот `robot-srch-releaser` состоит в этой abc-группе
* Роботы `robot-srch-releaser` и `robot-testenv` состоят в Sandbox-группе, которую указали при запуске задачи
* Проверяет, что есть/добавляет доступ Sandbox-группе до токена `common_release_token`

Далее запускается подзадача [`CreateNewRmForApphostVertical`](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/app_host/vertical_by_button/CreateNewRmForApphostVertical), которая создает конфиг для компоненты в [Release Machine](rm.z.yandex-team.ru/) ([документация по RM](https://wiki.yandex-team.ru/releasemachine/)) и все остальные необходимые файлы,
после чего мы ожидаем релиза задачи `ReleaseMachineConfigCrawler`, чтобы RM узнала о существовании нового конфига компоненты.
Далее запускаем [`CreateNannyServicesForApphostVertical`](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/app_host/vertical_by_button/CreateNannyServicesForApphostVertical/),
которая релизит компоненту в RM, создает все необходимые nanny-сервисы и awacs-балансер, после чего поднимает полученную вертикаль.

Более детальное описание задач `CreateNewRmForApphostVertical` и `CreateNannyServicesForApphostVertical` можно найти в их README.

Описание входных параметров доступно в документации [apphost'a](https://docs.yandex-team.ru/apphost/pages/new_vert#parametry-sandbox-zadachi-create_new_apphost_vertical).

## Откат изменений
Если вдруг по какой-то причине необходимо удалить все то, что `CreateNewApphostVertical`
создала непосильным трудом, можно воспользоваться задачей [`RemoveApphostVertical`](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/app_host/vertical_by_button/RemoveApphostVertical/).
