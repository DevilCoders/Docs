# nmaps_edits

Утилита подготовливает статистику по правкам пользователей NMAPS.

Расчитываются параметры:

* Количество уникальных правок
* Количество уникальных пользователей (которые эти правки сделали)
* количество уникальных отредактированных объектов

Результат фильтруется по 4 параметрам:

* Географический регион (страна, область, город и т.д.)
* Тип объектов (адреса, здания, дороги и т.д.)
* Тип операции (создание, редактирование, удаление)
* Роль пользователя (картограф, модератор, робот и т.д.)

Для расчета используются таблицы

* [Лог пользователей NMAPS][nmaps-users-dump-log]
* [Лог пользовательских правок][nmaps-edits-log]

Отчет в stat

* [Пользователи и правки][NmapUserCommit]

Скрипт автоматически запускается раз в день и делает расчет за вчерашнюю дату. [Reactor][reactor] и [граф в Nirvana][nirvana]

Расчет делается со `scale = 'daily'`. Агрегация по неделям, месяцам и годам выполняется в Statface.

Запуск руками:  `./nmaps_users_edit_count run --dates 2020-09-14 --proxy hahn --scale daily`

Раньше выполнялось в [QC](https://qc.yandex-team.ru/Node/771b7c88cb55fd07426dcda49f2eeb59), запускалось из [Хитмана][Hitman]

[nmaps-users-dump-log]: https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/nmaps-users-dump-log/1d
[nmaps-edits-log]: https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/nmaps-edits-log/1d
[NmapUserCommit]: https://stat.yandex-team.ru/Maps.Wiki/Others/NmapsAnalytics/NmapUserCommit
[reactor]: https://reactor.yandex-team.ru/reaction?id=7248967&mode=overview
[nirvana]: https://beta.nirvana.yandex-team.ru/flow/7cb3088a-ad9a-41fb-84fd-333cfbb97f73/c5af97ce-4e70-4c88-a7d5-9cdd91862dde/graph
[Hitman]: https://hitman.yandex-team.ru/projects/nmaps-beginners/nmaps-puid-editscount-create/?jobCreationTimeQuery=YEAR&jobPage=1&pageSize=20
