# CreateNewRmForApphostVertical

## Общее описание
Задача создает конфиг RM-компоненты для новой вертикали Apphost'a, в т.ч.:
* Создает соответствующую компоненту в [Release Machine](rm.z.yandex-team.ru/), [документация по RM](https://wiki.yandex-team.ru/releasemachine/).
* Создает классы всех необходимых Sandbox-ресуров для сборки данной компоненты.
* Добавляет все необходимые для apphost'a файлы в папку вертикали [`apphost/conf/verticals/<vertical_name>`](https://a.yandex-team.ru/arc/trunk/arcadia/apphost/conf/verticals/).
* Обновляет задачу `BuildHorizonAgentConfig`, добавляет в ее описание свежесозданные ресурсы.
* Добавляет ресурсы в файл `test_release_machine_components.py`.
* Создает для новой вертикали панель в [Woland](https://woland.n.yandex-team.ru), [документация по Woland](https://wiki.yandex-team.ru/woland/).

Рекомендуется запускать задачу не как самостоятельную, а при помощи [`CreateNewApphostVertical`](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/app_host/vertical_by_button/CreateNewApphostVertical/), которая ее породит как подзадачу.
Описание входных параметров доступно в документации [apphost'a](https://docs.yandex-team.ru/apphost/pages/new_vert#parametry-sandbox-zadachi-create_new_apphost_vertical), они совпадают с входными параметрами задачи [`CreateNewApphostVertical`](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/app_host/vertical_by_button/CreateNewApphostVertical/).
