# nmaps_count_revert_reason

Утилита подготовливает статистику по причинам отката правок модерации в NMAPS.

Расчитываются параметры:

* Количество уникальных правок модерации
* Количество уникальных правок модерации отдельно по статусу пользователя: модератор, яндекс модератор, картограф и т.д.

Результат фильтруется по 3 параметрам:

* Тип отката (vandalism, duplicate-creation, unreal-object-creation и т.д.)
* Тип объектов (адреса, здания, дороги и т.д.)
* Статус пользователя (модератор, яндекс-модератор, картограф и т.д.)

Для расчета используются таблицы

* [Лог пользователей NMAPS][nmaps-users-dump-log]
* [Лог модерации][nmaps-moderation-log]

Отчет в stat

* [Причины отката][NmapsModRevertReason]
* [Причины отката тест][NmapsModRevertReason_test]

Скрипт автоматически запускается раз в день и делает расчет за вчерашнюю дату. [Reactor][reactor] и [граф в Nirvana][nirvana]

Расчет делается со `scale = 'daily'`. Агрегация по неделям, месяцам и годам выполняется в Statface.

Запуск руками:  `./nmaps_count_resolved_users run --dates 2020-09-14 --proxy hahn --scale daily`

Раньше выполнялось в QC

[nmaps-users-dump-log]: https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/nmaps-users-dump-log/1d
[nmaps-moderation-log]: https://yt.yandex-team.ru/hahn/navigation?path=//logs/nmaps-moderation-log/1d
[NmapsModRevertReason]: https://stat.yandex-team.ru/Maps.Wiki/Others/NmapsAnalytics/NmapsModRevertReason
[NmapsModRevertReason_test]: https://stat-beta.yandex-team.ru/Maps.Wiki/Others/fricks/NmapsModRevertReason_test
[reactor]: https://reactor.yandex-team.ru/reaction?id=7248967&mode=overview
[nirvana]: https://beta.nirvana.yandex-team.ru/flow/7cb3088a-ad9a-41fb-84fd-333cfbb97f73/c5af97ce-4e70-4c88-a7d5-9cdd91862dde/graph
