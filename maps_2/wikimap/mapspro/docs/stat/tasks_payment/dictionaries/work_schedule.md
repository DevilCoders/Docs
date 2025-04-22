Графики работы сотрудников
==========================
[Зарплатные ведомости][accounting dashboard], подаваемые в бухгалтерию
отличаются для сотрудников, работающих на стандартном графике (стандартная
пятидневная неделя) и сотрудников с плавающими графиками.

Утилита [Work Schedule][] извлекает из OEBS признак стандартности графика для
каждого сотрудника из таблицы [staff dump][] и записывает его в таблицу [work
schedule][work schedule table].


Авторизация в OEBS
------------------
В OEBS используется TVM авторизация. Для авторизации со стороны Народной карты
используется TVM приложение [Work Schedule][TVM app] из ABC сервиса [Интеграция
Народной Карты и OEBS][abc].


[TVM app]:              https://abc.yandex-team.ru/services/nmaps_oebs_integration/resources/?show-resource=40066835
[Tasks Payment]:        https://stat.yandex-team.ru/Maps.Wiki/tasks_payment/Tasks_Payment
[Work Schedule]:        https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/stat/tasks_payment/dictionaries/work_schedule
[abc]:                  https://abc.yandex-team.ru/services/nmaps_oebs_integration/
[accounting dashboard]: https://datalens.yandex-team.ru/pap9drrtp1e2j-accounting-dashboard
[staff dump]:           https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/analytics/tasks_payment/dictionaries/staff_dump
[work schedule table]:  https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/analytics/tasks_payment/dictionaries/work_schedule_daily
