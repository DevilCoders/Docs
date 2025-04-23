| | |
|:------------- |:-------------:|
| Результат | Таблицы со стоимостью кликов в геопродуктовые организации [//home/maps/analytics/data/event-money/geoproduct/v0](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/analytics/data/event-money/geoproduct/v0) |
| Тикет | https://st.yandex-team.ru/GEOANALYTICS-809 |

Основной результат – таблицы [events-value-preliminary](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/analytics/data/event-money/geoproduct/v0/events-value-preliminary), он используются в дальнейших расчетах [event-money](https://wiki.yandex-team.ru/statbox/statkey/cubes/money/). Таблицы содержат клики на организации с геопродуктом и их оценочную стоимость.

Расчет состоит из двух этапов:
1. Оценка стоимости клика `permalink-cpa`
1. Формирование таблицы с кликами `events-value`

Расчеты делятся на два типа – быстрые (`preliminary`) и точные (`actual`).
- Быстрые считаются каждый день и используется оценка стоимости клика на основе исторических данных.
- Точные считаются при закрытии месяцы и используют фактические стоимости кликов
