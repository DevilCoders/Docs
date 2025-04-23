[Описание на Wiki](https://wiki.yandex-team.ru/maps/dev/core/wikimap/mapspro/feedbackkpi/#perexodnaaktualnyeinstrumentyiboleepodrobnoeopisanie)

## Задача агрегации данных для построения KPI-графиков фидбека

В [Дашборде Народной Карты](https://stat.yandex-team.ru/Dashboard/Nmaps?tab=10001) содержатся KPI-графики, связанные со скоростью разбора фидбека. График [Возраст открытого фидбека](https://charts.yandex-team.ru/preview/wizard/gradksov/age_percentile?workflow=feedback&kpi=3) сообщает о фидбеке, находящемся в процессе разбора. График [Длительность нахождения в статусе need-info](https://charts.yandex-team.ru/preview/iyfdp7dh9iy4e) описывает фидбек в состоянии "нужна информация". График [Возраст разобранных в каждый день перекрытий](https://charts.yandex-team.ru/preview/wizard/Users/gradksov/ClosureAgePercentile?workflow=feedback) содержит информацию об отдельном типе фидбека — перекрытиях дорожного движения — о возрасте перекрытий в момент разбора. Для каждого графика отображаются три значения — количество, максимальный возраст, 85-ый перцентиль возраста.

Данная задача позволяет производить расчет необходимых метрик за каждый день.

#### Входные данные

Агрегированные [таблицы feedback-2](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/analytics/feedback/db/feedback_latest) по элементам фидбека. В таблице за каждый день в дополнении к информации о самом фидбеке (тип, источник, геоточка) собирается информация о времени различных действий, произведенных с фидбеком и о пользователях, произведших эти действия — создание, публикация, закрытие, резолюция.

Необходимые для расчётов поля:
* id фидбека;
* iso_et_revealed — время публикации;
* type — тип;
* source — источник;
* workflow — фидбек/гипотеза;
* history — история действий с фидбеком.

#### Варианты использования

Для ежедневного дополнения графика в Nirvana заводится Reactive Workflow, производящий запуск задачи для одной отдельной даты: https://nirvana.yandex-team.ru/flow/b4ce64f3-e587-4c13-a780-1196533cae07.

Также существует возможность произвести локальный запуск с публикацией отчета и заданием диапазона дат. Необходимо собрать отдельный бинарник из исходного кода: [local_run](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/stat/feedback_age/bin/local_run).
