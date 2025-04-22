# nmaps_count_ui_blocks_ctr

Утилита подготовливает статистику по CTR блоков интерфейса НЯК.

Расчитываются параметры:

* Количество уникальных пользователей
* Количество уникальных пользователей, сделавших клик
* Количество уникальных пользователей, которые внесли какие-либо правки
* Количество уникальных пользователей, которые создали какой-либо объект
* Количество уникальных сессий работы
* Количество уникальных сессий работы с кликами
* Сумма кликов
* Сумма показов

Результат фильтруется по 4 параметрам:

* Географический регион (страна, область, город и т.д.)
* Тип действия (клик, показ, изменения зума и т.д.)
* Роль пользователя (картограф, модератор, робот и т.д.)

Для расчета используются таблицы:

* [Лог событий UI][common-redir-log]
* [Лог пользователей NMAPS][nmaps-users-dump-log]
* [Лог пользовательских правок][nmaps-edits-log]

Отчет в stat

* [CTR блоков UI в НЯК with user_path][nmaps_ui_bebr_CTR]

Скрипт автоматически запускается раз в день и делает расчет за вчерашнюю дату. [Reactor][reactor] и [граф в Nirvana][nirvana]

Расчет делается со `scale = 'daily'`. Агрегация по неделям, месяцам и годам выполняется в Statface.

Запуск руками:  `./nmaps_count_ui_blocks_ctr run --dates 2020-12-01 --proxy hahn --scale daily`

Раньше выполнялось в [QC](https://qc.yandex-team.ru/NodeGraph/4e13e271bb2b4d00b37c15050b94b412)

[common-redir-log]: https://yt.yandex-team.ru/hahn/navigation?path=//logs/common-redir-log/1d
[nmaps-users-dump-log]: https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/nmaps-users-dump-log/1d
[nmaps-edits-log]: https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/nmaps-edits-log/1d
[nmaps_ui_bebr_CTR]: https://stat.yandex-team.ru/Maps.Wiki/Others/NmapsAnalytics/nmaps_ui_bebr_CTR
[reactor]: https://reactor.yandex-team.ru/reaction?id=7248967&mode=overview
[nirvana]: https://beta.nirvana.yandex-team.ru/flow/7cb3088a-ad9a-41fb-84fd-333cfbb97f73/c5af97ce-4e70-4c88-a7d5-9cdd91862dde/graph
