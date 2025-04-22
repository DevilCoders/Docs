# nmaps_count_moderation_event_type

Утилита подготовливает статистику по типам промодерированных событий в NMAPS.

Расчитываются параметры:

* Количество уникальных правок модерации

Результат фильтруется по 3 параметрам:

* Статус пользователя (moderator, yandex-moderator, cartographer и т.д.)
* Тип объектов (адреса, здания, дороги и т.д.)
* Тип операции (complaint, edit, request-for-deletion)

Для расчета используются таблицы

* [Лог пользователей NMAPS][nmaps-users-dump-log]
* [Лог модерации][nmaps-moderation-log]

Отчет в stat

* [Тип модерируемого события][NmapsModEventType]
* [Тип модерируемого события тест][NmapsModEventType_test]

Скрипт автоматически запускается раз в день и делает расчет за вчерашнюю дату. [Reactor][reactor] и [граф в Nirvana][nirvana]

Расчет делается со `scale = 'daily'`. Агрегация по неделям, месяцам и годам выполняется в Statface.

Запуск руками:  `./nmaps_count_moderation_event_type run --dates 2020-09-14 --proxy hahn --scale daily`

Раньше выполнялось в QC

[nmaps-users-dump-log]: https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/nmaps-users-dump-log/1d
[nmaps-moderation-log]: https://yt.yandex-team.ru/hahn/navigation?path=//logs/nmaps-moderation-log/1d
[NmapsModEventType]: https://stat.yandex-team.ru/Maps.Wiki/Others/NmapsAnalytics/NmapsModEventType
[NmapsModEventType_test]: https://stat-beta.yandex-team.ru/Maps.Wiki/Others/fricks/NmapsModEventType_test
[reactor]: https://reactor.yandex-team.ru/reaction?id=7248967&mode=overview
[nirvana]: https://beta.nirvana.yandex-team.ru/flow/7cb3088a-ad9a-41fb-84fd-333cfbb97f73/c5af97ce-4e70-4c88-a7d5-9cdd91862dde/graph
