# nmaps_count_moderation_geo

Утилита подготовливает статистику по типам промодерированных событий в NMAPS.

Расчитываются параметры:

* Количесво уникальных отредактированных объектов
* Количество уникальных собственных правок
* Количество уникальных промодерированных правок
* Количество уникальных промодерированых объектов
* Наличие экспертных права пользователя на редактирование группы объектов
* Наличие модераторских прав пользователя на редактирование группы объектов
* Количество уникальных обработанных заданий на модерацию
* Длина сессии работы пользователя в Народной Карте
* Ссылка на пользоателя в Народной карте
* Количество уникальных заданий модерации, одобренных картографом
* Количество всех уникальных заданий модерации, обработанных картографом

Результат фильтруется по 3 параметрам:

* Географический регион (страна, область, город и т.д.)
* Статус пользователя (moderator, yandex-moderator, cartographer и т.д.)
* Тип объектов (адреса, здания, дороги и т.д.)
* Тип правки (import, commit-reverted, object_created и т.д.)

Для расчета используются таблицы

* [Лог пользователей NMAPS][nmaps-users-dump-log]
* [Лог модерации][nmaps-moderation-log]
* [Лог правок пользователей NMAPS][nmaps-edits-log]
* [Лог ролей пользователей NMAPS][nmaps-acl-roles-dump]

Отчет в stat

* [Модерация народной карты (geo)][NmapsModGeo]
* [Модерация народной карты (geo) тест][NmapsModGeo_test]

Скрипт автоматически запускается раз в день и делает расчет за вчерашнюю дату. [Reactor][reactor] и [граф в Nirvana][nirvana]

Расчет делается со `scale = 'daily'`. Агрегация по неделям, месяцам и годам выполняется в Statface.

Запуск руками:  `./nmaps_count_moderation_geo run --dates 2021-02-14 --proxy hahn --scale daily`

Раньше выполнялось в QC

[nmaps-users-dump-log]: https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/nmaps-users-dump-log/1d
[nmaps-moderation-log]: https://yt.yandex-team.ru/hahn/navigation?path=//logs/nmaps-moderation-log/1d
[nmaps-edits-log]: https://yt.yandex-team.ru/hahn/navigation?path=//logs/nmaps-edits-log/1d
[nmaps-acl-roles-dump]: https://yt.yandex-team.ru/hahn/navigation?path=//logs/nmaps-acl-roles-dump/1d
[NmapsModGeo]: https://stat.yandex-team.ru/Maps.Wiki/Others/NmapsAnalytics/NmapsModGeo
[NmapsModGeo_test]: https://stat-beta.yandex-team.ru/Maps.Wiki/Others/fricks/NmapsModGeo_test
[reactor]: https://reactor.yandex-team.ru/reaction?id=7248967&mode=overview
[nirvana]: https://beta.nirvana.yandex-team.ru/flow/7cb3088a-ad9a-41fb-84fd-333cfbb97f73/c5af97ce-4e70-4c88-a7d5-9cdd91862dde/graph
