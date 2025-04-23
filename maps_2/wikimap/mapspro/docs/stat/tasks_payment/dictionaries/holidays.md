Праздничные дни
===============
[Индивидуальные][private dashboard] и [менеджерский][manager dashboard] дашборды
учитывают работу в праздничные дни по увеличенному тарифу.

Информация о федеральных и региональных праздничных днях извлекается утилитой
[Holidays][tool] из OEBS и записывается в таблицу [holidays][] со следующей
структурой:
* `date` - дата, для которой эта таблица формируется;
* `staff_login` - логин сотрудника.

Информация о праздничных днях извлекается из OEBS для каждого сотрудника из
таблицы [staff dump][]. При этом записи в таблицу [holidays][] добавляются
только для тех сотрудников для кого этот день считается праздничным. В свою
очередь при расчёте отчёта [Tasks Payment][] для каждого сотрудника проверяется
наличие такой записи. Если запись есть, то этот день считается праздничным и к
тарифу применяется повышающий коэффициент.

Авторизация в OEBS
------------------
В OEBS используется TVM авторизация. Для авторизации со стороны Народной карты
используется TVM приложение [Holidays][TVM app] из ABC сервиса [Интеграция
Народной Карты и OEBS][abc].


[TVM app]:              https://abc.yandex-team.ru/services/nmaps_oebs_integration/resources/?show-resource=41376779
[Tasks Payment]:        https://stat.yandex-team.ru/Maps.Wiki/tasks_payment/Tasks_Payment
[abc]:                  https://abc.yandex-team.ru/services/nmaps_oebs_integration/
[accounting dashboard]: https://datalens.yandex-team.ru/pap9drrtp1e2j-accounting-dashboard
[holidays]:             https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/analytics/tasks_payment/dictionaries/holidays
[manager dashboard]:    https://datalens.yandex-team.ru/it29j3u4v4d4e-piecework-dashboard-manager
[private dashboard]:    https://datalens.yandex-team.ru/k0vdpvk3sue0g-piecework-dashboard-employee
[staff dump]:           https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/analytics/tasks_payment/dictionaries/staff_dump
[tool]:                 https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/stat/tasks_payment/dictionaries/holidays
