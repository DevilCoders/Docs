Обработка логов сервиса masstransit-predictor
---

Процесс обрабатывает таблички с логами сервиса maps-core-masstransit-predictor и создает на их основе таблички с предсказаниями прибытий на остановки для расчета онлайн-качества. В процессе обработки записи лога дедуплицируются, а также эмулируется задержка экстатика.

### Результаты

[Тестинг](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/testing/masstransit/forecasts/arrivals)<br>
[Продакшн](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/masstransit/forecasts/arrivals)
