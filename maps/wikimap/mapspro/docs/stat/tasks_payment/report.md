Отчёт Tasks Payment
===================
Отчёт формируется утилитой [Tasks Payment Cartographic Report][tasks payment] и
находится в Stat-е по адресу: [Maps.Wiki/tasks_payment/Tasks_Payment][report].


Отображение в зарплатной ведомости всех действующих сотрудников
---------------------------------------------------------------
[Зарплатная ведомость][accounting dashboard] должна содержать всех действующих
сотрудников, в том числе и тех, кто не выполнял никаких работ в текущем периоде,
например, из-за отпуска.  Ведомость формируется запросом к отчёту [Tasks
Payment][], и если в некотором периоде у сотрудника нет выполненных работ, то
срез отчёта не будет содержать его имени.

Для отображения всех действующих сотрудников, во время расчёта отчёта [Tasks
Payment][] формируется "лог работ" содержащий технические записи. Для каждого
действующего на дату формирования отчёта сотрудника, в этот лог добавляется
"работа" с `task_id = service/current-employee`. Сформированный лог подаётся на
вход на равне с другими логами работ. Таким образом, любой срез отчёта содержит
всех действующих в выбранном периоде сотрудников.

Список действующих сотрудников формируется на основе таблицы [staff dump][]. Для
этих целей таблица содержит колонку `quit_at` с датой увольнения
сотрудника. `puid` сотрудника берётся из таблицы [linked accounts][].

{% note alert %}

Действующими считаются только сотрудники с привязанным к Стаффу логином Народной
карты.

{% endnote %}

К техническим записям, описанным выше, применяется нулевой тариф.


Надбавка за работу в праздничные дни
------------------------------------
Работа в праздничные дни оплачивается по увеличенным тарифам.

[Зарплатная ведомость][accounting dashboard] для сотрудников со стандартным
графиком подаётся в рублях и не корректируется на стороне бухгалтерии. Кроме
того, [менеджерский][piecework manager] и [персональные][piecework employee]
дашборды сдельщиков отображают сумму в рублях которую сотрудник получит на руки
(до вычета налогов). Поэтому применение коэффициента за работу в праздничные дни
происходит в момент формирования отчёта.

[Зарплатная ведомость][accounting dashboard] для сотрудников с плавающим
графиком подаётся в базовых оценках. Базовые оценки, за работу выполненную в
обычные и праздничные дни, попадают в разные колонки ведомости (благодаря
показателю `holiday` отчёта [Tasks Payment][report]). А коэффициент за работу в
праздничные дни применяется на стороне бухгалтерии.


[accounting dashboard]: https://datalens.yandex-team.ru/pap9drrtp1e2j-accounting-dashboard
[linked accounts]:      https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/analytics/tasks_payment/dictionaries/linked_accounts
[piecework employee]:   https://datalens.yandex-team.ru/k0vdpvk3sue0g-piecework-dashboard-employee
[piecework manager]:    https://datalens.yandex-team.ru/it29j3u4v4d4e-piecework-dashboard-manager
[report]:               https://stat.yandex-team.ru/Maps.Wiki/tasks_payment/Tasks_Payment
[staff dump]:           https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/analytics/tasks_payment/dictionaries/staff_dump
[tasks payment]:        https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/stat/tasks_payment/reports/cartographic_report
