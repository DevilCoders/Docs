Что это такое
===
Здесь лежит код для расчёта статистики мобильных геоприложений (МЯК, Навигатор, Таксометр)

В директории external лежат расчеты для внешних пользователей
В директории hypgen лежат внутренние инструменты от аналитиков для генерации гипотез

Архитектура
===
![Основные элементы](./docs/img/metrics.png)


Расчёт статистик запускается ежедневно, по мере готовности исходных таблиц.

Основные сущности, участвующие в вычислении статистики:
===
### Препроцессор
Препроцессор - регулярный процесс, отвечающий за подготовку сырых данных к  нужному нам виду.

На вход принимает сырые таблицы метрики и таблицы с локейшенами.

Результатом являются cooked-таблицы

Препроцессор
1) фильтрует из исходных таблиц необходимые поля
2) размечает DrivingSessions, т.е. поездки из точки А в точку Б
3) размечает UserSessions - т.е. сессии активного использования приложения
4) присваивает событиям список экспериментов
5) размечает тип ведения

Результат работы препроцессора (cooked-таблицы) используется
1) непосредственно для вычисления различных метрик
2) визуализации поездок стендом ((https://a.yandex-team.ru/arc_vcs/maps/tools/navi-stat-vis Navi-Stat-Vis))
3) для ручных аналитических вычислений

### Метрики
Основным потребителем cooked-таблиц являются Метрики.
Все посчитанные таблицы лежат в [//home/maps/statistics](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/statistics)

Большинство метрик (но не все, есть возможность гибкой настройки, например, можно подключать дополнительные таблицы, генерируемые внешними регулярными процессами) выполнены по следующей схеме:
1) делается reduce по полю DrivingSerssionID по cooked-таблице. Внутри редьюса агрегируются все необходимые величины.
2) результатом работы является таблица с значениями метрик для каждого DrivingSessionID


| DrivingSessionID | Metric 1 | Metric 2 |
|------------------|----------|----------|
| id1 | m1_value1 | m2_value1 |
| id2 | m1_value2 | m2_value2 |

Такие таблицы лежат, в основном, в папке aggregated_by_sessions,
Основными потребителями этих таблиц являются  DataLens и КоФе.

Потребители таблиц
===
### DataLens
По посчитанным метриками таблицам сделаны дашборды в DataLens.
| Приложение | Дашборды |
|------------|----------|
| Навигатор | [Автомобильные метрики](https://datalens.yandex-team.ru/r94e7e0wg6wgm-metriki-navigacii)<br>[Автомобильные метрики (тестинг)](https://datalens.yandex-team.ru/5j88bxa1kveiz-metriki-navigacii-testing) |
| МЯК | [Автомобильные метрики](https://datalens.yandex-team.ru/j7g305rgf5foe-metriki-myak)<br>[Пешеходные метрики](https://datalens.yandex-team.ru/6u7as3wbxwcez-metriki-masstransit) |
| Таксометр | |

### CoFe
Вторым большим потребителем посчитанных метриками таблиц является система проведения А/Б экспериментов [Cofe](https://wiki.yandex-team.ru/serp/experiments/cofe/doc/).

Ежедневно из таблиц, посчитанных метриками, запускается расчёт прекомпьютов (предпосчитанные величины для всех метрик по всем выборкам).
Далее в [админке](https://ab.yandex-team.ru/) создаётся наблюдение с указанными выборками.

Код для расчёта метрик в Кофе лежит в Аркадии по адресу:
[quality/ab_testing/cofe/projects/mapkit](https://a.yandex-team.ru/arc_vcs/quality/ab_testing/cofe/projects/mapkit)

Пути и ссылки
===
### Компоненты
| Компонент | Путь в Аркадии |
|-----------|----------------|
|Препроцессор|[maps/statistics/log_preprocessor](https://a.yandex-team.ru/arc_vcs/maps/statistics/log_preprocessor)|
|Метрики|[maps/statistics/metrics](https://a.yandex-team.ru/arc_vcs/maps/statistics/metrics)|


### Таблицы на yt
| Приложение | Исходные таблицы | Cooked-таблицы | Cooked-таблицы (тестинг) | Метрики |
|------------|------------------|----------------|--------------------------|---------|
| Навигатор | [//home/logfeller/logs/navi-metrika-mobile-log/1d](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/navi-metrika-mobile-log/1d)<br><br>[//home/logfeller/logs/appmetrica-location-log/1d](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/appmetrica-location-log/1d) | [//home/maps/analytics/logs/cooked-metrika-mobile-log/navi](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/analytics/logs/cooked-metrika-mobile-log/navi) | [//home/maps/analytics/logs/cooked-metrika-mobile-log.6p/navi](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/analytics/logs/cooked-metrika-mobile-log.6p/navi) | [//home/maps/statistics/navi](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/statistics/navi) |
| МЯК | [//home/logfeller/logs/appmetrica-yandex-events/1d](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/appmetrica-yandex-events/1d)<br><br>[//home/logfeller/logs/appmetrica-location-log/1d](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/appmetrica-location-log/1d) | [//home/maps/analytics/logs/cooked-metrika-mobile-log/mobile-maps](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/analytics/logs/cooked-metrika-mobile-log/mobile-maps) | [//home/maps/analytics/logs/cooked-metrika-mobile-log.6p/mobile-maps](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/analytics/logs/cooked-metrika-mobile-log.6p/mobile-maps) | [//home/maps/statistics/mobile-maps](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/statistics/mobile-maps) |
| Таксометр | [//home/logfeller/logs/taxi-metrika-mobile-log/1d](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/taxi-metrika-mobile-log/1d)<br><br>[//home/logfeller/logs/appmetrica-location-log/1d](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/appmetrica-location-log/1d) | [//home/maps/analytics/logs/cooked-metrika-mobile-log/taximeter](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/analytics/logs/cooked-metrika-mobile-log/taximeter) | [//home/maps/analytics/logs/cooked-metrika-mobile-log.6p/taximeter](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/analytics/logs/cooked-metrika-mobile-log.6p/taximeter) | [//home/maps/statistics/taximeter](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/statistics/taximeter) |
