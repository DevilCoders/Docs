# nmaps_count_mapsprpo_layers

Утилита подготовливает статистику по промодерированным объектам в NMAPS.

Расчитываются параметры:

* Количество уникальных правок модерации
* Количество уникальных правок модерации отдельно по статусу пользователя: модератор, яндекс модератор, картограф

Результат фильтруется по 3 параметрам:

* Географический регион (страна, область, город и т.д.)
* Тип объектов (адреса, здания, дороги и т.д.)
* Тип операции (complaint, edit, request-for-deletion)

Для расчета используются таблицы

* [Лог пользователей NMAPS][nmaps-users-dump-log]
* [Дамп-лог ролей пользователей][nmaps-acl-roles-dump]

Отчет в stat

* [Послойники (new)][NmapsMapsprpoLayers]
* [Послойники (new) тест][NmapsMapsprpoLayers_test]

Скрипт автоматически запускается раз в день и делает расчет за вчерашнюю дату. [Reactor][reactor] и [граф в Nirvana][nirvana]

Расчет делается со `scale = 'daily'`. Агрегация по неделям, месяцам и годам выполняется в Statface.

Запуск руками:  `./nmaps_count_mapsprpo_layers run --dates 2020-09-14 --proxy hahn --scale daily`

Раньше выполнялось в QC

[nmaps-users-dump-log]: https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/nmaps-users-dump-log/1d
[nmaps-acl-roles-dump]: https://yt.yandex-team.ru/hahn/navigation?path=//logs/nmaps-acl-roles-dump/1d
[NmapsMapsprpoLayers]: https://stat.yandex-team.ru/Maps.Wiki/Others/NmapsAnalytics/NmapsMapsprpoLayers
[NmapsMapsprpoLayers_test]: https://stat-beta.yandex-team.ru/Maps.Wiki/Others/fricks/NmapsMapsprpoLayers_test
[reactor]: https://reactor.yandex-team.ru/reaction?id=7248967&mode=overview
[nirvana]: https://beta.nirvana.yandex-team.ru/flow/7cb3088a-ad9a-41fb-84fd-333cfbb97f73/c5af97ce-4e70-4c88-a7d5-9cdd91862dde/graph
[Hitman]: https://hitman.yandex-team.ru/projects/nmaps-beginners/nmaps-puid-editscount-create/?jobCreationTimeQuery=YEAR&jobPage=1&pageSize=20
