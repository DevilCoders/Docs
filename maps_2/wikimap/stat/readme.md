Инструменты для построения отчетов в народных картах
====================================================

Мониторинги
-----------

### Отчёт Tasks Payment
- мониторинг копирования данных Трекера (очереди MAPSPW и OUTKARTPW) в YT: [`host=tracker, service=sync_to_yt`][juggler-tracker-to-yt].
- мониторинг копирования таблиц схемы `social` из PostgreSQL в YT: [`host=solomon-alert, service=nmaps_dynamic_replica_social`][juggler-social-to-yt].

Смотри также [описание мониторингов][Tasks Payment monitorings].


### Отчёт Assessment
- мониторинг копирования таблиц схемы `assessment` из PostgreSQL в YT: [`host=solomon-alert, service=nmaps_dynamic_replica_assessment`][juggler-assessment-to-yt].

Смотри также [описание генератора отчёта][Assessment monitorings].


### Отчёт Nmaps Feedback
- мониторинг копирования таблиц fbapi из PostgreSQL в YT: [`host=solomon-alert, service=nmaps_dynamic_replica_fbapi`][juggler-fbapi-to-yt]


Инструменты
-----------
Рекомендуется использовать стек:
- [YT][yt], кластер [hahn][hahn] - расчеты и хранение всех данных
- [Nile][nile] - описание расчета в терминах map/reduce операций на YT, + публикация на stat
- Nile [CLI][cli] (используется не во всех отчетах) - удобный способ использовать один и тот же код и для локального запуска, и в операциях в Nirvana
- [Nirvana][nirvana] - платформа для облачного выполнения расчетов
- [Reactor][reactor] - автоматизация регулярных запусков отчетов
- [Statface][statface] - хранение и отображение отчетов
- [Dash][dash] - дашборды, обеспечивающие удобные срезы, таблицы и графики по отчетам


### Исходные данные
Исходные данные отчетов лежат в YT. Если не лежат - сначала нужно найти способ принести их в YT.
Мы используем кластер Hahn. Для тех данных, которые мы складываем в YT сами, используется
[//home/maps/core/nmaps/analytics](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/analytics).
Логи, приносимые логфеллером, лежат в [//home/logfeller/logs/](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs).
Данные трекера -- в [//home/startrek/tables/prod/yandex-team/common](https://yt.yandex-team.ru/hahn/navigation?path=//home/startrek/tables/prod/yandex-team/common). Рядом же лежат дампы заказанных очередей.


### Описание расчета
Описание расчета происходит в двух местах - в Nirvana задается граф операций, в репозитории хранится код, который в этих операциях выполняется.
Хранение в репозитории позволяет поддерживать ревью кода, написание тестов, локальные запуски инструментов.
Граф расчета в Nirvana лучше поддерживать максимально простым.


### Workflow расчета в Nirvana
Все шаги отчета описываются графом операций/кубиков в нирване.

Основной используемый кубик - [Nile][nile cube], исполняющий py-скрипт (или бинарник), написанный с использованием библиотеки Nile, оформленный совместимым способом

Код на вход кубика в нашиз расчетах попадает в виде аркадийного бинарника.
Иногда, для тестовых расчетов, может использоваться возможность задавать скрипт непосредственно в текстовом параметре кубика, или ссылкой на скрипт в аркадии.

Для сборки аркадийного проекта используется Nirvana-кубик [Build Arcadia Project][build aarcadia project]. На выходе -  исполняемый Nile-скрипт (в нашем случае).
Может быть две стратегии релиза
- зафиксировать ревизию и обновлять ее в параметрах кубика вручную
- каждый раз собирать проект заново, используя последнюю ревизию аркадии. Соответственно, все изменения применяются сразу после коммита в транк.
Для получения ревизии можно использовать официальный кубик [get arcadia revision][get arcadia revision].
У нас используется альтернативный самостоятельно собранный [select revision][select revision].

Расчеты обычно опираются на текущую(или "вчерашнюю") дату запуска.
Чтобы при перезапуске упавшего расчета дата не съехала, ее нужно фиксировать.
Для этого удобно передавать дату из реакции `global yesterday = Context.cronScheduledTime().plusDays(-1).format("yyyy-MM-dd");`, например
Например, расчет [Tasks Payment][tasks payment].
В расчете [Valuable Edits][valuable edits] используется другой способ.
Там сегодняшняя/вчерашняя даты генерируются в самом начале графа отдельными кубиками, и при рестарте после падения расчета в последующих кубиках
используются уже сгенерированные даты. Но граф становится заметно более громоздким.


### Код расчета
Для описания операции расчета и публикации используется Nile CLI и питон.

В скрипте расчета задаются источники данных и последовательность nile-операций над ними - взять таблицу A, пересечь с таблицей B по полю cc, отфильтровать результат по условию dd > 0, оставить только колонки ee и ff, результат записать в таблицу C. [Пример в документации](https://logos.yandex-team.ru/statbox/nile/).
Это описание превратится в набор map/reduce операций и будет выполняться на указанном кластере.
При необходимости можно описать на питоне кастомные функции фильтрации и map/reduce операции.

При использовании Nile cli расчет описывается внутри функции со стандартным `@cli.statinfra_job()` декоратором, например, https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/stat/tasks_payment/tasks_logging/feedback/bin/main.py.


### Локальный запуск
При использовании Nile CLI при локальном запуске бинарника локально создается граф расчета, а выполнение происходит на удаленном кластере.
Обязательные аргументы --proxy, а так же --scale и --dates, даже если они не используются в расчете. Можно передавать свои аргументы.
Локальный запуск имеет вид
`./nile_script run --proxy hahn --scale daily --dates 2020-01-01 2020-01-02`


### Тестирование
При описании nile-графа расчета для результата любой операции можно задать метку. Например, см. функцию https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/stat/tasks_payment/tasks_logging/feedback/lib/feedback_log.py make_feedback_log_job
При тестировании можно проверять не только полный граф расчета, но и любой частичный подграф, начинающийся
со входящих меток и заканчивающийся результирующими. Остальные части расчёта будут пропущены.
В тестах нужно задать входные таблицы и канонический вариант выходной таблицы. Потом остается сверить результат с каноническим, обычно с применением сортировки. Например, https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/stat/tasks_payment/tasks_logging/feedback/tests/tests.py.


### Краткий Style guide
Проект расчета обычно разделяется на три части
- тривиальный bin, задающий Nile CLI `main` и `make_job` с декоратором.
- lib, описывающие расчет, вызываемый из `bin.make_job`
- tests, тесты, проверяющие все шаги расчета по отдельности и вместе
плюс тривиальный, по возможности, граф в нирване.

При описании расчета удобно структурировать все этапы расчета, оформляя все шаги отдельными функциями, в комментариях описывая формат всех входных и выходных данных, например https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/stat/tasks_payment/tasks_logging/feedback/lib/feedback_log.py.


### Регулярный запуск
Для регулярного запуска задач используются [hitman] (не рекомендуется) или [reactor].
Запуск должен производиться из-под робота robot-wikimap.
В параметрах nile-кубика нужно будет указать `YT Token`.
Если скрипт еще и публикует отчет в statface, то и `Statface token`.
Токены можно найти на странице [Nirvana Secrets][nirvana secrets] поиском по `robot-wikimap`.

Вместо коммунального пула следует использовать пул 'maps-nmaps-mapreduce'.
Иногда это может радикально улучшить производительность.
Пул задается в поле `YT Pool` кубика nile.


[yt]: https://yt.yandex-team.ru
[hahn]: https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/analytics
[nirvana]: https://wiki.yandex-team.ru/nirvana/manual
[nile]: https://logos.yandex-team.ru/statbox/nile/
[nile cube]: https://clubs.at.yandex-team.ru/statistics/1388/
[cli]: https://clubs.at.yandex-team.ru/statistics/943
[statface]: https://stat.yandex-team.ru
[dash]: https://dash.yandex-team.ru
[hitman]: https://wiki.yandex-team.ru/hitman/documentation
[reactor]: https://wiki.yandex-team.ru/nirvana/reactor
[build aarcadia project]: https://nirvana.yandex-team.ru/operation/95ddb9b8-8777-4946-a015-1737e4219317

[select revision]: https://nirvana.yandex-team.ru/operation-old/38f0022c-0962-4cca-940e-2a41e890ebfa/overview
[get arcadia revision]: https://nirvana.yandex-team.ru/operation/6de29046-455a-4a76-af66-96feef0f836f
[tasks payment]: https://nirvana.yandex-team.ru/browse?selected=6046235
[valuable edits]: https://nirvana.yandex-team.ru/flow/538f58fb-a040-40af-9334-c3b995969a8c/17184d22-2789-4449-83c7-e30ea38803da/graph
[nirvana secrets]: https://nirvana.yandex-team.ru/secrets

[Assessment monitorings]: https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/stat/assessment/report/readme.md#monitorings
[Tasks Payment monitorings]: https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/stat/tasks_payment/docs/monitorings.md

[juggler-social-to-yt]: https://juggler.yandex-team.ru/check_details/?host=solomon-alert&service=nmaps_dynamic_replica_social
[juggler-tracker-to-yt]: https://juggler.yandex-team.ru/check_details/?host=tracker&service=sync_to_yt
[juggler-assessment-to-yt]: https://juggler.yandex-team.ru/check_details/?host=solomon-alert&service=nmaps_dynamic_replica_assessment
[juggler-fbapi-to-yt]: https://juggler.yandex-team.ru/check_details/?host=solomon-alert&service=nmaps_dynamic_replica_fbapi
