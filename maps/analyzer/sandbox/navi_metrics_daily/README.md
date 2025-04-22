Подсчет метрик по логам навигатора
---

Регулярный процесс подсчета метрик по логам навигатора.
Считает метрики для каждого города и всех регионов уровнем выше (объемлющих). Соот-но полные метрики можно получить по региону "Земля" (10000).

Сессия учитывается в регионе, в котором она была больше всего (по кол-ву пингов), пинги же попадают в свои регионы.

Вычисляемые метрики: см. [таблицу](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/navi-metrics-daily/metrics)

### Результаты
* [метрики](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/navi-metrics-daily/metrics)
* [пинги](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/navi-metrics-daily/pings)
* [сессии](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/navi-metrics-daily/sessions)
* [евенты](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/navi-metrics-daily/events)
### Ссылки
* [бэкап статбокса](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/navi-metrics-daily/metrics/archive)
* [панель на дашборде](https://datalens.yandex-team.ru/5q70qk3wf8ww2-probki?tab=aEq)

#### Заметки

 * `last_estimated_ping_time` - прогнозируемое время до следующего пинга
 * `initial_estimated_time_on_route` - спрогнозированное время от начала маршрута до текущего пинга
